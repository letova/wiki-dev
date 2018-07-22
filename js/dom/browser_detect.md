# Browser detect

```javascript
const ua = navigator.userAgent;

const browsersDetectionData = {
    opera: {
        get name() {
            return new RegExp('OPR', 'i').test(ua) ? 'OPR' : 'Opera';
        },
        check: () => (!!window.opr && !!opr.addons) || !!window.opera || ua.indexOf(' OPR/') >= 0
    },
    firefox: {
        name: 'Firefox',
        check: () => typeof InstallTrigger !== 'undefined'
    },
    safari: {
        name: 'Safari',
        check: () => {
            return /constructor/i.test(window.HTMLElement) || 
            (function (p) { return p.toString() === "[object SafariRemoteNotification]"; })(!window['safari'] || safari.pushNotification) ||
            /^((?!chrome|android).)*safari/i.test(ua)
        }
    },
    ie: {
        name: 'MSIE', 
        check: () => /*@cc_on!@*/false || !!document.documentMode
    },
    edge: {
        name: 'Edge', 
        check: () => !document.documentMode && !!window.StyleMedia
    },
    chrome: {
        name: 'Chrome', 
        check: () => !!window.chrome && !!window.chrome.webstore
    }
};

const getBrowserVersion = (browser, ua) => {
    const index = ua.indexOf(browser);

    if (index === -1) {
        return;
    }

    return parseFloat(ua.substring(index + browser.length + 1)); 
};


const browserIdentificator = Object.keys(browsersDetectionData).filter(browser => browsersDetectionData[browser].check());

const browserName = browsersDetectionData[browserIdentificator].name;

const browserVersion = getBrowserVersion(browserName, ua);
```