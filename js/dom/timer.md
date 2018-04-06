# Timer

## Отсчет с нуля MM:SS

```
<div class="container"></div>
<button class="stop-timer">Stop</button>
```

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

        stopButton.addEventListener('click', function() {
            clearInterval(interval);
        });
        
    }, 1000);
  
};
```

```javascript
const container = document.querySelector('.container');
const stopButton = document.querySelector('.stop-timer');
timer(container, stopButton);
```