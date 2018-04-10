# Timer

## Отсчет с нуля MM:SS

*HTML*
```
<div class="container"></div>
<button class="stop-timer">Stop</button>
```

*JS*
```javascript
const timer = (container, stopButton) => {
    let secondsCounter = 0;
  
    const interval = setInterval(function () {
        secondsCounter += 1;
        
        let minutes = Math.floor(secondsCounter / 60);
        let seconds = secondsCounter - (minutes * 60);
        
        if (minutes < 10) minutes = '0' + minutes;
        if (seconds < 10) seconds = '0' + seconds;
        
        container.innerHTML = `${minutes}:${seconds}`;
        
    }, 1000);

    stopButton.addEventListener('click', function() {
        clearInterval(interval);
    });
  
};
```

```javascript
const container = document.querySelector('.container');
const stopButton = document.querySelector('.stop-timer');
timer(container, stopButton);
```

## Обратного отсчета DAY HH:MM:SS

*HTML*
```
<div class="container"></div>
```

*JS*
```javascript
const timer = (container, date) => {
    const endDate = new Date(...date);
    
    const interval = setInterval(function () {
    	const currentDate = new Date();
    	const timeDistance = (endDate - currentDate) / 1000;
    
        let days = Math.floor(timeDistance / 86400);
        let hours = Math.floor(timeDistance / 3600) % 24;
        let minutes = Math.floor(timeDistance / 60) % 60;
        let seconds = Math.floor(timeDistance % 60);
        
        if (hours < 10) hours = '0' + hours;
        if (minutes < 10) minutes = '0' + minutes;
        if (seconds < 10) seconds = '0' + seconds;

        const dayWord = (hours > 4 || hours === 0) ? 'дней' : (hours > 1) ? 'дня' : 'день';

        container.innerHTML = `Осталось ${days} ${dayWord} ${hours}:${minutes}:${seconds}`;
    
    }, 1000);
};
```

```javascript
const container = document.querySelector('.container');
timer(container, [2018, 03, 10, 19, 53]); // отсчет месяца начинается с 0!
```