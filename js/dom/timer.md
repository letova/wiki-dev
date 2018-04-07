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