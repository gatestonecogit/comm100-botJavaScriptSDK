## Introduction

Bot JavaScript SDK is used to connect Comm100 Live Chat Visitor Side and 3rd party systems.

For example, Comm100 Chatbot can send a form to visitors for collecting information. The form can be the built-in form with custom fields or a fully custom form from your webpage. If you are using your own form, you can set values, submit form or get chatbot variables with the SDK.

## Installation

To use the SDK, please copy and paste the following code into the form webpage before the closing `</body>` tag

```javascript
<!-- Begin BotJavaScriptSDK Code -->
<script type="text/javascript">
    var url = "https://vue.comm100.com/visitorside/js/botJavaScriptSDK.js";
    var BotJavaScriptSDK = BotJavaScriptSDK || {};
    (function (t) {
    function e(e) {
        var a = document.createElement("script"),
        c = document.getElementsByTagName("script")[0];
        (a.type = "text/javascript"),
        (a.async = !0),
        (a.src = e),
        c.parentNode.insertBefore(a, c);
    }
    e(url);
    setTimeout(function () {
        t.loaded || e(url);
    }, 5e3);
    })(BotJavaScriptSDK);
</script>
<!-- End BotJavaScriptSDK Code -->
```

## How to use the SDK

It's recommended to wrap your call with a callback function that is assigned to BotJavaScriptSDK.onReady.

```javascript
BotJavaScriptSDK.onReady = function () {
  // use SDK here safely
};
```

## What the SDK provides

Bot JavaScript SDK provides 3 functions: Get, Set and Do.

### Get

To get information from chatbot, you can use BotJavaScriptSDK.get:

```javascript
/**
 * @param {string} type - Type of data to get, you can find all types in doc below.
 * @return {any} result.
 */
BotJavaScriptSDK.get("bot.variables");
```

### Set

To set value to chatbot variable, you can use BotJavaScriptSDK.set:

```javascript
/**
 * @param {string} type - Type of data to set, you can find all types in doc below.
 * @param {any} value - Value that will be set.
 */
BotJavaScriptSDK.set("bot.variable", {
  name: "Name",
  value: "xxx",
});
```

### Do

To submit a form or close form page, you can use BotJavaScriptSDK.do:

```javascript
/**
 * @param {string} type - Type of action to do, you can find all types in doc below.
 * @param {any} value - Value that will be send.
 * finished successfully or not.  nothing will be returned.
 */
var name = "xxx";
var email = "xxx@xxx.com";
BotJavaScriptSDK.do(
  "bot.sendForm.submit",
  `submit success! \n name: ${name} \n email: ${email}`
);
```

## Reference

### Site ID 

```javascript
const siteId = BotJavaScriptSDK.get(`livechat.siteId`);
```

### Campaign ID

```javascript
const campaignId = BotJavaScriptSDK.get(`livechat.campaignId`);
```

### Chat Id 

```javascript
const chatId = BotJavaScriptSDK.get(`livechat.chatId`);
```

### Bot info 

```javascript
const botInfo = BotJavaScriptSDK.get("bot.botInfo");
```

### Get or Set Custom Variable

```javascript
const customVariables = BotJavaScriptSDK.get("livechat.customVariables");
/**
 * @return
 * [
 *  {
 *   name: "custom variable 1",
 *   value: "current value",
 *  },
 *  {
 *   name: "non-existant custom variable",
 *   value: "current value",
 *  }
 * ]
 */

const values = [
  {
    name: "custom variable 1",
    value: "current value",
  },
  {
    name: "non-existant custom variable",
    value: "current value",
  },
  {
    name: "ignored custom variable",
  },
];
BotJavaScriptSDK.set("livechat.customVariables", values);
```

### Get or Set Bot variables 

```javascript
const collectValues = BotJavaScriptSDK.get("bot.variables");
/**
 * @return
 * {
 *   "variableName1": "variable value",
 *   "variableName2": ["variable value1", "variable value2"],
 *   "variableName3": {
 *                       "key1": "value",
 *                       "key2": "value2"
 *                    }
 * }
 */
BotJavaScriptSDK.set("bot.variable", {
    {
        name: "variableName1",
        value: "variable value",
    }
});
BotJavaScriptSDK.set("bot.variable", {
    {
        name: "variableName2",
        value: ["variable value1", "variable value2"],
    }
});
BotJavaScriptSDK.set("bot.variable", {
    {
        name: "variableName3",
        value:  {
                    "key1": "value",
                    "key2": "value2"
                },
    }
});
```

### Get visitor Info 

```javascript
const visitorInfo = Comm100APICrossMessage.get("bot.visitorInfo");
/**
 * @return
 * {
 *   name: "",
 *   email: "",
 *   phone: "",
 *   company: "",
 *   product: "",
 *   department: "",
 *   ticketId: "",
 *   ...
 * }
 */
```

### Submit data

```javascript
var name = "xxx";
var email = "xxx@xxx.com";
BotJavaScriptSDK.do(
  "bot.sendForm.submit",
  `submit success! \n name: ${name} \n email: ${email}`
);
```

### Close webView 

```javascript
BotJavaScriptSDK.do("bot.sendForm.close");
```
