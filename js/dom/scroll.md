# Scroll

## Скролл к нижней точке документа

```javascript
const getPosition = (element) => {
    var box = element.getBoundingClientRect();
    return {
        top: box.top + window.pageYOffset, 
        left: box.left + window.pageXOffset,
        scrollTop: window.pageYOffset,
        scrollLeft: window.pageXOffset
    };
};

const scrollDown = (startElement, speed) => {
    const startY = getPosition(startElement).scrollTop;
    const stopY = Math.max(document.body.scrollHeight, document.documentElement.scrollHeight) - document.documentElement.clientHeight;

    const distance = stopY - startY;
    
    let step = 20;
    let stepNumber = Math.ceil(distance / step); 
    let traveledDistance = 0;

    if (traveledDistance < distance) {

        for (let i = 1; i <= stepNumber; i += 1) {
            if (step > (distance - traveledDistance)) {
                step = distance - traveledDistance;
            }

            traveledDistance += step;

            if (traveledDistance < 40) {
                speed += 5;
            }

            setTimeout(window.scrollTo, i * speed, 0, startY + traveledDistance);
        }
    }
};
```