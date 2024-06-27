package com.db.axiom.sparta.utils.timezone;

import com.db.axcore.utils.PrimitiveNulls;
import com.db.axiom.appscore.workflow.ActionComponent;
import com.db.axiom.base.workflow.actions.FormatUtils;
import com.db.axiom.bob.TimeInForce;
import com.db.axiom.sparta.bob.SpartaOrder;
import com.db.axiom.sparta.utils.BusinessDaysCalendar;
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;

import java.time.Clock;
import java.time.Instant;
import java.time.LocalDate;
import java.time.LocalDateTime;
import java.time.LocalTime;
import java.time.ZoneId;
import java.time.ZonedDateTime;
import java.time.temporal.ChronoUnit;
import java.util.Map;
import java.util.Optional;

/**
 * This class provides time zone aware methods for computing date to long conversions.
 * All dates will represent local dates at start of day, will be stored as milliseconds and will be displayed relative to UTC timezone.
 * All timestamps will represent UTC timestamps stored as milliseconds or microseconds and will be displayed relative to user timezone
 */
@ActionComponent
public class DateTimeUtils {
    private static final Logger LOG = LoggerFactory.getLogger(DateTimeUtils.class);
    private static final ZoneId UTC = ZoneId.of(FormatUtils.DEFAULT_TIME_ZONE);
    private static final int DEFAULT_SETTLE_DAYS = 2;

    private Clock clock;
    private Map<String, String> exDestinationMap = null;

    public DateTimeUtils(Clock clock) {
        this.clock = clock;
    }

    public void setClock(Clock clock) {
        this.clock = clock;
    }

    public LocalTime getLocalTime() {
        return LocalTime.now(clock);
    }

    public ZoneId getLocalTimeZone() {
        return clock.getZone();
    }

    public LocalDate today() {
        return LocalDate.now(clock);
    }

    public long currentTimeMillis() {
        return LocalDateTime.now(clock).atZone(getLocalTimeZone()).toInstant().toEpochMilli();
    }

    public void setExDestinationMap(Map exDestinationMap) {
        this.exDestinationMap = exDestinationMap;
    }

    /**
     * Default trade date to current local date
     * @return current timezone date at start of day in UTC milliseconds
     */
    public long defaultTradeDateMillis() {
        return LocalDate.now(clock)
                .atStartOfDay(UTC)
                .toInstant().toEpochMilli();
    }

    /**
     * Default settlement date as 2 business days after trade date
     * @param tradeDateMillis trade date as UTC milliseconds
     * @return settlement date milliseconds at start of day
     */
    public long defaultSettlDateMillisBasedOnTradeDate(long tradeDateMillis) {
        if (PrimitiveNulls.isNull(tradeDateMillis)) {
            LOG.warn("TradeDate is not set. Cannot default SettlDate");
            return PrimitiveNulls.NULL_LONG;
        }
        LocalDate tradeDate = FormatUtils.utcDateFromMillis(tradeDateMillis);
        LocalDate defaultSettleDate = BusinessDaysCalendar.plusBusinessDays(tradeDate, DEFAULT_SETTLE_DAYS);
        return defaultSettleDate.atStartOfDay(UTC).toInstant().toEpochMilli();
    }

    /**
     * Extract local date in current timezone from timestamp milliseconds
     * @param utcTimestampMillis timestamp milliseconds
     * @return local date at start of day
     */
    public long dateMillisFromUtcTimestampMillis(long utcTimestampMillis) {
        return regionDateFromMillis(utcTimestampMillis)
                .atStartOfDay(UTC)
                .toInstant().toEpochMilli();
    }

    public long dateMillisFromUtcTimestampMicros(long timestampMicros, String exDestination) {
        if (this.exDestinationMap != null && this.exDestinationMap.get(exDestination) != null) {
            String timeZone = this.exDestinationMap.get(exDestination);
            ZonedDateTime dateTime = Instant.ofEpochMilli(timestampMicros / 1000).atZone(ZoneId.of(timeZone));
            return dateTime.toLocalDate().atStartOfDay(UTC).toInstant().toEpochMilli();
        }
        return PrimitiveNulls.NULL_LONG;
    }

    /**
     * Extract local date in current timezone from timestamp microseconds
     * @param timestampMicros timestamp microseconds
     * @return local date at start of day
     */
    public long dateMillisFromUtcTimestampMicros(long timestampMicros) {
        return dateMillisFromUtcTimestampMillis(timestampMicros / 1000);
    }

    /**
     * Checks if an order should expire based on its expire date or expire time
     * @param eventTimeUtcMillis timestamp of expiry check
     * @param order sparta order
     * @return true/false
     */
    public boolean isOrderInScopeForExpire(long eventTimeUtcMillis, SpartaOrder order) {
        if (order.getTimeInForce() == TimeInForce.GTC.getFixValue()) {
            return false;
        }
        if (order.getTimeInForce() == TimeInForce.DAY.getFixValue()) {
            return true;
        }
        LocalDateTime eventDateTime = LocalDateTime.ofInstant(Instant.ofEpochMilli(eventTimeUtcMillis), getLocalTimeZone());
        LocalDateTime expireDateTime = getRegionAwareExpireDateTime(order).orElse(null);

        if (expireDateTime == null) {
            return false;
        }

        return !eventDateTime.isBefore(expireDateTime);
    }

    private Optional<LocalDateTime> getRegionAwareExpireDateTime(SpartaOrder order) {
        LocalDateTime regionExpireDateTime = null;

        if (!PrimitiveNulls.isNull(order.getExpireTime())) {
            regionExpireDateTime = Instant.ofEpochMilli(order.getExpireTime() / 1000).atZone(getLocalTimeZone()).toLocalDateTime();
        } else if (!PrimitiveNulls.isNull(order.getExpireDate())) {
            LocalDate regionExpireDate = FormatUtils.utcDateFromMillis(order.getExpireDate());
            regionExpireDateTime = regionExpireDate.atTime(LocalTime.MAX); // Assuming end of day for expireDate
        }
        return Optional.ofNullable(regionExpireDateTime);
    }

    /**
     * Timezone aware business date expressed as a given number of days in the future from today
     * @param numberOfDays number of business days in the future
     * @return local date at start of day
     */
    public long todayPlusBusinessDays(int numberOfDays) {
        return BusinessDaysCalendar.plusBusinessDays(today(), numberOfDays)
                .atStartOfDay(UTC)
                .toInstant().toEpochMilli();
    }

    public long yesterdayPlusBusinessDays(int numberOfDays) {
        return BusinessDaysCalendar.plusBusinessDays(today().minusDays(1), numberOfDays)
                .atStartOfDay(UTC)
                .toInstant().toEpochMilli();
    }

    /**
     * Converts a number of milliseconds to a local date in the current timezone
     * @param milliseconds date milliseconds
     * @return local date
     */
    public LocalDate regionDateFromMillis(long milliseconds) {
        return Instant.ofEpochMilli(milliseconds).atZone(clock.getZone()).toLocalDate();
    }

    public long getDaysUntil(long untilDate) {
        LocalDate regionToday = today();
        LocalDate regionUntilDate = FormatUtils.utcDateFromMillis(untilDate);
        return regionToday.until(regionUntilDate, ChronoUnit.DAYS);
    }

    public long getDaysAlive(long creationDateTime) {
        LocalDate regionToday = today();
        LocalDate regionCreationDate = regionDateFromMillis(creationDateTime / 1000);
        return regionCreationDate.until(regionToday, ChronoUnit.DAYS);
    }

    public long todayPlusBusinessDaysAtTimeInMillis(int numberOfDays, LocalTime time) {
        return ZonedDateTime.of(BusinessDaysCalendar.plusBusinessDays(today(), numberOfDays)
                .atTime(time), getLocalTimeZone()).toInstant().toEpochMilli();
    }
}
