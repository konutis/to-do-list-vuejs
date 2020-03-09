<template>
  <div class='date-container'>
    <p class='date-main'>{{weekDay}}, {{date}}</p>
    <p class='date-month'>{{month}}</p>
  </div>
</template>

<script>
    export default {
        name: 'DateBar',
        data: () => {
            const monthNames = ['January', 'February', 'March', 'April', 'May', 'June', 'July', 'August', 'September', 'October', 'November', 'December']
            const days = ['Sunday', 'Monday', 'Tuesday', 'Wednesday', 'Thursday', 'Friday', 'Saturday']
            const date = new Date()
            const nth = function(d) {
                if (d > 3 && d < 21) return 'th'
                switch (d % 10) {
                    case 1:  return "st"
                    case 2:  return "nd"
                    case 3:  return "rd"
                    default: return "th"
                }
            }
            const calendarDate = date.getDate()

            return {
                month: monthNames[date.getMonth()],
                weekDay: days[date.getDay()],
                date: calendarDate + nth(calendarDate)
            }
        }
    }
</script>
