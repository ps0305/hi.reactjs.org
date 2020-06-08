---
id: hooks-faq
title: Hooks FAQ
permalink: docs/hooks-faq.html
prev: hooks-reference.html
---

*Hooks* React 16.8 में जोड़ा गया है जो, आपको बिना क्लास कॉम्पोनेन्ट के स्टेट और अन्य React फीचर्स का उपयोग करने देते हैं

यह पृष्ठ [Hooks](/docs/hooks-overview.html) के बारे में अक्सर पूछे जाने वाले प्रश्नों के उत्तर देता है

<!--
  if you ever need to regenerate this, this snippet in the devtools console might help:

  $$('.anchor').map(a =>
    `${' '.repeat(2 * +a.parentNode.nodeName.slice(1))}` +
    `[${a.parentNode.textContent}](${a.getAttribute('href')})`
  ).join('\n')
-->

* **[एडॉप्शन स्ट्रेटेजी](#adoption-strategy)**
  * [React के कौन से संस्करणों में hooks शामिल हैं?](#which-versions-of-react-include-hooks)
  * [क्या मुझे अपने सभी क्लास कॉम्पोनेन्ट को फिर से लिखना होगा?](#do-i-need-to-rewrite-all-my-class-components)
  * [मैं Hooks के साथ क्या कर सकता हूं जो मैं क्लासेज के साथ नहीं कर सकता हूं?](#what-can-i-do-with-hooks-that-i-couldnt-with-classes)
  * [मेरा React ज्ञान कितना प्रासंगिक है?](#how-much-of-my-react-knowledge-stays-relevant)
  * [क्या मुझे Hook, क्लासेज या दोनों का मिश्रण इस्तेमाल करना चाहिए?](#should-i-use-hooks-classes-or-a-mix-of-both)
  * [क्या Hooks, क्लासेज के सारे उपयोगों को कवर करता है?](#do-hooks-cover-all-use-cases-for-classes)
  * [क्या Hooks रेंडर प्रॉप्स और हायर आर्डर कंपोनेंट्स को रेप्लस करता है?](#do-hooks-replace-render-props-and-higher-order-components)
  * [पॉपुलर APIs जैसे Redux connect() और React Router के लिए रियेक्ट के मायने?](#what-do-hooks-mean-for-popular-apis-like-redux-connect-and-react-router)
  * [क्या Hooke स्टैटिक टाइपिंग के साथ काम करता है?](#do-hooks-work-with-static-typing)
  * [Hooks का इस्तेमाल करते वाले कंपोनेंट्स का टेस्ट कैसे करें?](#how-to-test-components-that-use-hooks)
  * [लिंट नियम क्या लागू करते हैं?](#what-exactly-do-the-lint-rules-enforce)
* **[क्लासेज से हूक्स तक](#from-classes-to-hooks)**
  * [लाइफ साइकिल मेथड्स Hooks को कैसे करेस्पॉन्ड करते हैं?](#how-do-lifecycle-methods-correspond-to-hooks)
  * [Hooks के द्वारा डाटा फेचिंग कैसे करें?](#how-can-i-do-data-fetching-with-hooks)
  * [क्या इंस्टैंस वेरिएबल की तरह कुछ है?](#is-there-something-like-instance-variables)
  * [एक या एक से ज्यादा स्टेट वेरिएबल का इस्तेमाल करना चाहिए?](#should-i-use-one-or-many-state-variables)
  * [क्या इफेक्ट को सिर्फ उपडटेस के बाद इस्तेमाल करना चाहिए?](#can-i-run-an-effect-only-on-updates)
  * [पिछले प्रॉप्स या स्टेट को कैसे प्राप्त करें?](#how-to-get-the-previous-props-or-state)
  * [पुराने स्टेट्स और प्रॉप्स का फंक्शन में दिखने का क्या मतलब है?](#why-am-i-seeing-stale-props-or-state-inside-my-function)
  * [getDerivedStateFromProps कैसे इम्प्लीमेंट करें?](#how-do-i-implement-getderivedstatefromprops)
  * [क्या forceUpdate जैसा कुछ है?](#is-there-something-like-forceupdate)
  * [क्या फंक्शन कम्पोनेंट क लिए ref बना सकते हैं?](#can-i-make-a-ref-to-a-function-component)
  * [DOM नोड को कैसे मापेंगे?](#how-can-i-measure-a-dom-node)
  * [const [thing, setThing क्या करते हैं] = useState() mean?](#what-does-const-thing-setthing--usestate-mean)
* **[परफॉरमेंस ऑप्टिमिजाशंस](#performance-optimizations)**
  * [क्या अपडेट पर एक इफ़ेक्ट स्किप कर सकते हैं?](#can-i-skip-an-effect-on-updates)
  * [क्या डेपेंडेन्सीज़ की सूची से फंक्शन्स को छोड़ना सुरक्षित है?](#is-it-safe-to-omit-functions-from-the-list-of-dependencies)
  * [इफ़ेक्ट डेपेंडेन्सीज़ के बार बार बदलने की दशा में क्या करें?](#what-can-i-do-if-my-effect-dependencies-change-too-often)
  * [shouldComponentUpdate कैसे इम्प्लीमेंट करें?](#how-do-i-implement-shouldcomponentupdate)
  * [कॅल्क्युलेशन्स को कैसे मेमोइज़ी करें?](#how-to-memoize-calculations)
  * [एक्सपेंसिव ऑब्जेक्ट को लॉज़ीली कैसे क्रिएट करें?](#how-to-create-expensive-objects-lazily)
  * [क्या रेंडर में फंक्शन क्रिएट करने की वजह से Hooks धीमा है?](#are-hooks-slow-because-of-creating-functions-in-render)
  * [कॉलबॉक्स को डाउन पास करने से कैसे बचें?](#how-to-avoid-passing-callbacks-down)
  * [से बार बार बदलती हुई एक वैल्यू को कैसे रीड करें?](#how-to-read-an-often-changing-value-from-usecallback)
* **[अंडर द हुड](#under-the-hood)**
  * [कंपोनेंट्स के साथ React सहयोगी हुक कैसे कॉल करता है?](#how-does-react-associate-hook-calls-with-components)
  * [Hooks के लिए पूर्व कला क्या है?](#what-is-the-prior-art-for-hooks)

## एडॉप्शन स्ट्रेटेजी {#adoption-strategy}

### React के कौन से संस्करणों में hooks शामिल हैं? {#which-versions-of-react-include-hooks}

16.8.0 के साथ शुरू, React में React Hooks का एक स्थिर इम्प्लीमेंटेशन शामिल है:

* React DOM
* React Native
* React DOM Server
* React Test Renderer
* React Shallow Renderer

ध्यान दें **hook को इस्तेमाल करने के लिए, सभी React पैकेज 16.8.0 या उच्चतर होना चाहिए**. यदि आप अपडेट करना भूल जाते हैं तो hook काम नहीं करेंगे, उदाहरण के लिए, React DOM.

[React Native 0.59](https://reactnative.dev/blog/2019/03/12/releasing-react-native-059) और उच्चतर हुक को सपोर्ट करते हैं।

### क्या मुझे अपने सभी क्लास कॉम्पोनेन्ट को फिर से लिखना होगा? {#do-i-need-to-rewrite-all-my-class-components}

नहीं, रियेक्ट से क्लासेज को हटाने का [कोई प्लान](/docs/hooks-intro.html#gradual-adoption-strategy) नहीं है, हम सभी को शिपिंग उत्पादों को रखने की आवश्यकता है और वे फिर से लिखे नहीं जा सकते।
हम नए कोड में हुक को शामिल करने की सलाह देते हैं।

### मैं Hooks के साथ क्या कर सकता हूं जो मैं क्लासेज के साथ नहीं कर सकता हूं? {#what-can-i-do-with-hooks-that-i-couldnt-with-classes}

["अपनी खुद की हुक का निर्माण"](/docs/hooks-custom.html) विभिन्न संभावनाओं की एक झलक प्रदान करता है। हुक कंपोनेंट्स के बीच फंक्शनलिटी का री-यूज़ करने के लिए एक शक्तिशाली और नया एक्सप्रेसिव तरीका प्रदान करते हैं. ["लेख"](https://medium.com/@dan_abramov/making-sense-of-react-hooks-fdbde8803889) में एक रिएक्ट कोर टीम के सदस्य द्वारा हुक द्वारा अनलॉक की गई नई क्षमताओं पर गहन अध्ययन।

### मेरा React ज्ञान कितना प्रासंगिक है? {#how-much-of-my-react-knowledge-stays-relevant}

हुक, आपके द्वारा पहले से ही पहचाने जाने वाले रिएक्ट फीचर्स का उपयोग करने के लिए एक अधिक सीधा तरीका है - जैसे कि स्टेट ,लाइफसाइकिल, रेफ्स और कॉन्टेक्स्ट । वे मूल रूप से परिवर्तन नहीं करते हैं कि रिएक्ट कैसे काम करता है, और आपके कंपोनेंट्स, प्रॉप्स और टॉप-डाउन डेटा प्रवाह का ज्ञान पूरी तरह से प्रासंगिक है।

हुक्स का अपना लर्निंग कर्व है. यदि इस डॉक्यूमेंटेशन में कुछ कमी है,तो [इशू रेज करें](https://github.com/reactjs/reactjs.org/issues/new) और हम मदद करने की कोशिश करेंगे।

### क्या मुझे Hook, क्लासेज या दोनों का मिश्रण इस्तेमाल करना चाहिए? {#should-i-use-hooks-classes-or-a-mix-of-both}

जब आप तैयार हों, तो हम आपके द्वारा लिखे गए नए कंपोनेंट्स में हुक इम्प्लीमेंट की कोशिश करने के लिए प्रोत्साहित करेंगे। सुनिश्चित करें कि आपकी टीम में हर कोई उन्हें इस्तेमाल करने और इस डॉक्यूमेंटेशन से परिचित हों। जब तक आप उन्हें फिर से लिखने की योजना नहीं बनाते, हम आपके पहले से उपस्थित क्लासेज को हुक्स का इस्तेमाल कर के लिखने के लिए प्रोत्साहित नहीं करते(जैसे बग को ठीक करने के लिए)।

आप एक क्लास कॉम्पोनेन्ट *के अंदर हुक* का उपयोग नहीं कर सकते हैं, लेकिन आप निश्चित रूप से एक ही ट्री में हुक के साथ क्लासेज और फ़ंक्शन कंपोनेंट्स को मिला सकते हैं। एक कॉम्पोनेन्ट एक क्लास या एक फ़ंक्शन है जो हुक का उपयोग करता है, उस कॉम्पोनेन्ट का कार्यान्वयन विवरण है। लंबी अवधि में, हम उम्मीद करते हैं कि प्राथमिक रूप से लोग के रिएक्ट कॉम्पोनेन्ट लिखने का तरीका हुक्स बनेगा।

### क्या Hooks, क्लासेज के सारे उपयोगों को कवर करता है? {#do-hooks-cover-all-use-cases-for-classes}

हमारा लक्ष्य हुक के लिए जितनी जल्दी हो सके क्लासेज के सभी उपयोग के मामलों को कवर करना है। असामान्य `getSnapshotBeforeUpdate`, ` getDerivedStateFromError` और `componentDidCatch` लाइफसाइकिल के लिए कोई हुक समकक्ष नहीं हैं, लेकिन हम जल्द ही इसे जोड़ने की योजना बना रहे हैं।

यह हुक के लिए एक प्रारंभिक समय है, और कुछ थर्ड-पार्टी लाइब्रेरीज इस समय हुक के अनुरूप नहीं हो सकते हैं।

### क्या Hooks रेंडर प्रॉप्स और हायर आर्डर कंपोनेंट्स को रेप्लस करता है? {#do-hooks-replace-render-props-and-higher-order-components}

अक्सर, प्रॉप्स और उच्च-क्रम के कॉम्पोनेन्ट केवल एक ही चाइल्ड को प्रस्तुत करते हैं। हमें लगता है कि हुक इस उपयोग के मामले को पूरा करने का एक सरल तरीका है। दोनों पैटर्न के लिए अभी भी एक जगह है (उदाहरण के लिए, एक वर्चुअल स्कॉलर कंपोनेंट में एक `renderItem` 'प्रोप हो सकता है, या एक विज़ुअल कंटेनर कंपोनेंट की अपनी DOM स्ट्रक्चर हो सकती है)। लेकिन ज्यादातर मामलों में, हुक पर्याप्त होंगे और आपके ट्री में नेस्टिंग काम करने में मदद करेंगे।

### पॉपुलर APIs जैसे Redux connect() और React Router के लिए रियेक्ट के मायने? {#what-do-hooks-mean-for-popular-apis-like-redux-connect-and-react-router}

आप हमेशा के समान सटीक API का उपयोग जारी रख सकते हैं, वे काम करेंगे।

React Redux V7.1.0 के बाद से [हुक्स API का सपोर्ट करते हैं](https://react-redux.js.org/api/hooks) और `useDispatch` or `useSelector` जैसे हुक्स एक्सपोज़ करते हैं।

React Router v5.1 के बाद से [हुक्स का सपोर्ट करते हैं](https://reacttraining.com/react-router/web/api/Hooks) 

अन्य लाइब्रेरीज भी भविष्य में हुक का समर्थन कर सकते हैं।

### क्या Hook स्टैटिक टाइपिंग के साथ काम करता है? {#do-hooks-work-with-static-typing}

हुक को स्टैटिक टाइपिंग को ध्यान में रखकर डिजाइन किया गया था। क्योंकि वे कार्य कर रहे हैं, वे उच्च-क्रम के कंपोनेंट्स जैसे पैटर्न की तुलना में सही प्रकार से लिखना आसान है। नवीनतम फ्लो और टाइपस्क्रिप्ट रिएक्ट डेफिनिशंस में रिएक्ट हुक के लिए समर्थन शामिल है।

महत्वपूर्ण बात यह है कि कस्टम हुक आपको React API को बाधित करने की शक्ति देता है यदि आप उन्हें किसी तरह से अधिक सख्ती से टाइप करना चाहते हैं। रिएक्ट आपको प्रिमितिवेस देता है, लेकिन आप उन्हें अलग-अलग तरीकों से जोड़ सकते हैं जो हम लीक से हटकर प्रदान करते हैं।

### Hooks का इस्तेमाल करते वाले कंपोनेंट्स का टेस्ट कैसे करें? {#how-to-test-components-that-use-hooks}

रिएक्ट के दृष्टिकोण से, हुक का उपयोग करने वाला एक कॉम्पोनेन्ट सिर्फ एक रेगुलर कॉम्पोनेन्ट है। यदि आपका टेस्ट समाधान रिएक्ट इंटर्नल्स पर निर्भर नहीं करता है, तो हुक के साथ टेस्टिंग कम्पोनेंट आपको सामान्य रूप से कम्पोनेंट्स का टेस्ट करने के तरीके से अलग नहीं होना चाहिए।

> ध्यान दें
>
> [टेस्टिंग रेसिपीज](/docs/testing-recipes.html) कई उदाहरणों को शामिल करते हैं जिन्हें आप कॉपी और पेस्ट कर सकते हैं

उदाहरण के लिए, मान लें कि हमारे पास यह काउंटर कॉम्पोनेन्ट है:

```js
function Example() {
  const [count, setCount] = useState(0);
  useEffect(() => {
    document.title = `You clicked ${count} times`;
  });
  return (
    <div>
      <p>You clicked {count} times</p>
      <button onClick={() => setCount(count + 1)}>
        Click me
      </button>
    </div>
  );
}
```

हम रिएक्ट डोम का उपयोग करके इसका टेस्ट करेंगे। यह सुनिश्चित करने के लिए कि ब्राउज़र में क्या बिहेवियर है, हम कोड रेंडरिंग को व्रैप और [ReactTestUtils.act()](/docs/test-utils.html#act) कॉल में अपडेट करेंगे:

```js{3,20-22,29-31}
import React from 'react';
import ReactDOM from 'react-dom';
import { act } from 'react-dom/test-utils';
import Counter from './Counter';

let container;

beforeEach(() => {
  container = document.createElement('div');
  document.body.appendChild(container);
});

afterEach(() => {
  document.body.removeChild(container);
  container = null;
});

it('can render and update a counter', () => {
  // Test first render and effect
  act(() => {
    ReactDOM.render(<Counter />, container);
  });
  const button = container.querySelector('button');
  const label = container.querySelector('p');
  expect(label.textContent).toBe('You clicked 0 times');
  expect(document.title).toBe('You clicked 0 times');

  // Test second render and effect
  act(() => {
    button.dispatchEvent(new MouseEvent('click', {bubbles: true}));
  });
  expect(label.textContent).toBe('You clicked 1 times');
  expect(document.title).toBe('You clicked 1 times');
});
```

`act()` के लिए कॉल भी उनके अंदर इफ़ेक्ट फ्लश जाएगा.

यदि आपको एक कस्टम हुक का टेस्ट करने की आवश्यकता है, तो आप अपने टेस्ट में एक कॉम्पोनेन्ट बनाकर, और उसमें अपने हुक का उपयोग करके ऐसा कर सकते हैं। फिर आप लिखे गए कॉम्पोनेन्ट का टेस्ट कर सकते हैं।

बॉयलरप्लेट को कम करने के लिए, हम [रियेक्ट टेस्टिंग लाइब्रेरी](https://testing-library.com/react) का उपयोग करने की सलाह देते हैं जो टेस्ट राइटिंग को प्रोत्साहित करने के लिए डिज़ाइन किया गया है जो आपके कंपोनेंट्स का उपयोग एन्ड यूजर के रूप में करते हैं।

अधिक जानकारी के लिए [टेस्टिंग रेसिपीज़](/docs/testing-recipes.html) चेक करें।

### [लिंट नियम](https://www.npmjs.com/package/eslint-plugin-react-hooks) क्या लागू करते हैं? {#what-exactly-do-the-lint-rules-enforce}

हम बग्स से बचने के लिए एक प्लग-इन  [ESLint plugin](https://www.npmjs.com/package/eslint-plugin-react-hooks) जो [हुक्स के रूल्स](/docs/hooks-rules.html) लागू करते हैं। यह मानता है कि कोई भी फ़ंक्शन "`use`" और एक कैपिटल लेटर के बाद के शुरू होने वाला एक हुक है। हम पहचानते हैं कि यह अनुमान सही नहीं है और कुछ गलत सकारात्मक हो सकते हैं, लेकिन पारिस्थितिकी तंत्र के व्यापक सम्मेलन के बिना, हुक को अच्छी तरह से काम करने का कोई तरीका नहीं है - और लंबे समय तक लोग हुक को अपनाने या सम्मेलन का पालन करने से लोगों को हतोत्साहित करेंगे।

विशेष रूप से, नियम लागू होता है:

* हुक कॉल या तो एक `PascalCase` फ़ंक्शन (एक कॉम्पोनेन्ट माना जाता है) या किसी अन्य` useSomething` फ़ंक्शन (एक कस्टम हुक माना जाता है) के अंदर हैं।
* हुक हर रेंडर पर एक ही क्रम में कॉल किया जाता है।

कुछ और आंकड़े हैं, और वे समय के साथ बदल सकते हैं क्योंकि हम झूठी सकारात्मकता से बचने के साथ बग को खोजने के लिए नियम को ठीक करते हैं।

## क्लासेज से हूक्स तक {#from-classes-to-hooks}

### लाइफ साइकिल मेथड्स Hooks को कैसे करेस्पॉन्ड करते हैं? {#how-do-lifecycle-methods-correspond-to-hooks}

* `constructor`: फ़ंक्शन कंपोनेंट्स को कंट्रक्टर की आवश्यकता नहीं है। आप [`useState`] (/ डॉक्स / हुक-संदर्भ.html # usestate) कॉल में इनिशियलाइज़ कर सकते हैं। यदि इनिशियल स्थिति की कंप्यूटिंग करना महंगा है, तो आप एक फ़ंक्शन को 'useState' में पास कर सकते हैं।

* `getDerivedStateFromProps`: इसके बजाय [रेंडर करते हुए](#how-do-i-implement-getderivedstatefromprops) को अपडेट शेड्यूल करें।

* `shouldComponentUpdate`: `React.memo` [देखें](#how-do-i-implement-shouldcomponentupdate).

* `render`: यह फंक्शन कंपोनेंट बॉडी है.

* `componentDidMount`, `componentDidUpdate`, `componentWillUnmount`: The [`useEffect` Hook](/docs/hooks-reference.html#useeffect) can express all combinations of these (including [less](#can-i-skip-an-effect-on-updates) [common](#can-i-run-an-effect-only-on-updates) cases).

* `getSnapshotBeforeUpdate`, `componentDidCatch` और `getDerivedStateFromError`: इन विधियों के लिए कोई हुक समकक्ष नहीं हैं, लेकिन उन्हें जल्द ही जोड़ दिया जाएगा।

### Hooks के द्वारा डाटा फेचिंग कैसे करें {#how-can-i-do-data-fetching-with-hooks}

आपकी शुरुआत के लिए एक [छोटा डेमो](https://codesandbox.io/s/jvvkoo8pq3). अधिक जानने के लिए, हुक के साथ डेटा फेच के बारे में [यह लेख](https://www.robinwieruch.de/react-hooks-fetch-data/) देखें।

### या इंस्टैंस वेरिएबल की तरह कुछ है? {#is-there-something-like-instance-variables}

हाँ, [useRef()](/docs/hooks-reference.html#useref) हुक केवल एक डॉम रेफ्स नहीं है। `ref` ऑब्जेक्ट एक सामान्य कंटेनर है, जिसका `current` प्रॉपर्टी परस्पर भिन्न होता है और किसी क्लास पर एक उदाहरण प्रॉपर्टी के समान किसी भी वैल्यू को होल्ड सकता है।

आप इसे `useEffect` के अंदर से लिख सकते हैं:

```js{2,8}
function Timer() {
  const intervalRef = useRef();

  useEffect(() => {
    const id = setInterval(() => {
      // ...
    });
    intervalRef.current = id;
    return () => {
      clearInterval(intervalRef.current);
    };
  });

  // ...
}
```

अगर हम सिर्फ एक इंटरवल निर्धारित करना चाहते हैं, तो हमें रेफ की आवश्यकता नहीं होगी (`id` इफ़ेक्ट के लिए लोकल हो सकती है), लेकिन यह उपयोगी है अगर हम एक इवेंट  हैंडलर से इंटरवल को क्लियर करना चाहते हैं।:

```js{3}
  // ...
  function handleCancelClick() {
    clearInterval(intervalRef.current);
  }
  // ...
```
वैचारिक रूप से, आप किसी क्लास में वेरिएबल के समान रेफ के बारे में सोच सकते हैं। जब तक आप [लेज़ी इनिशियलएसशन](#how-to-create-expensive-objects-lazily) नहीं कर रहे हैं, रेंडरिंग के दौरान रिफ सेट करने से बचें - इससे आश्चर्यजनक व्यवहार हो सकता है। इसके बजाय, आमतौर पर आप ईवेंट हैंडलर और इफ़ेक्ट्स में Refs को संशोधित कर सकते हैं। 

### एक या एक से ज्यादा स्टेट वेरिएबल का इस्तेमाल करना चाहिए? {#should-i-use-one-or-many-state-variables}

यदि आप क्लासेज का यूज़ करते आ रहे हैं, तो आपको हमेशा एक बार `useState()` को कॉल करने और सभी स्टेट को एक ही ऑब्जेक्ट में डालने की कोशिश कर के सामान बिहेवियर पाने की कोशिश करनी चाहिए। आप चाहें तो ऐसा कर सकते हैं। यहां एक कॉम्पोनेन्ट का उदाहरण है जो माउस मूवमेंट  फॉलो करता है। हम इसकी पोजीशन और साइज को लोकल स्टेट में रखते हैं:

```js
function Box() {
  const [state, setState] = useState({ left: 0, top: 0, width: 100, height: 100 });
  // ...
}
```

अब मान लें कि हम कुछ तर्क लिखना चाहते हैं जो यूजर के माउस को स्थानांतरित करने पर `left` और `top` बदलता है। ध्यान दें कि हमें इन फ़ील्ड्स को पिछली स्टेट  ऑब्जेक्ट में मैन्युअल रूप से कैसे मर्ज करना है:

```js{4,5}
  // ...
  useEffect(() => {
    function handleWindowMouseMove(e) {
      // Spreading "...state" ensures we don't "lose" width and height
      setState(state => ({ ...state, left: e.pageX, top: e.pageY }));
    }
    // Note: this implementation is a bit simplified
    window.addEventListener('mousemove', handleWindowMouseMove);
    return () => window.removeEventListener('mousemove', handleWindowMouseMove);
  }, []);
  // ...
```

ऐसा इसलिए है क्योंकि जब हम किसी स्टेट वैरिएबल को अपडेट करते हैं, तो हम उसकी वैल्यू को *रिप्लेस* करते हैं। यह एक क्लास में `this.setState` से अलग है, जो ऑब्जेक्ट में अपडेटेड फ़ील्ड को *मर्ज* करता है।

यदि आप आटोमेटिक मर्जिंग को मिस करते हैं, तो आप एक कस्टम `useLegacyState` हुक लिख सकते हैं जो ऑब्जेक्ट स्टेट अपडेट को मर्ज करता है। हालाँकि, **हम स्टेट को कई स्टेट वेरिएबल में विभाजित करने की सलाह देते हैं जिसके आधार पर वैल्यू एक साथ बदलते हैं।**

उदाहरण के लिए, हम अपने कंपोनेंट स्टेट को `position` और `size` ऑब्जेक्ट्स में विभाजित कर सकते हैं, और हमेशा `position` को बदलने की आवश्यकता नहीं है:

```js{2,7}
function Box() {
  const [position, setPosition] = useState({ left: 0, top: 0 });
  const [size, setSize] = useState({ width: 100, height: 100 });

  useEffect(() => {
    function handleWindowMouseMove(e) {
      setPosition({ left: e.pageX, top: e.pageY });
    }
    // ...
```

इंडिपेंडेंट स्टेट वेरिएबल को अलग करने का एक और लाभ भी है। उदाहरण के लिए, कस्टम हुक में बाद में कुछ संबंधित लॉजिक को एक्सट्रेक्ट करना आसान बनाता है:

```js{2,7}
function Box() {
  const position = useWindowPosition();
  const [size, setSize] = useState({ width: 100, height: 100 });
  // ...
}

function useWindowPosition() {
  const [position, setPosition] = useState({ left: 0, top: 0 });
  useEffect(() => {
    // ...
  }, []);
  return position;
}
```

ध्यान दें कि हम अपने कोड को बदले बिना एक कस्टम हुक में `position` स्टेट वेरिएबल और रिलेटेड इफ़ेक्ट के लिए `useState` कॉल को कैसे मूव करने में सक्षम थे। यदि सभी स्टेट एक ही ऑब्जेक्ट में थे, तो इसे निकालना अधिक कठिन होगा।

सभी स्टेट एक `useState` कॉल में रखने, और प्रत्येक फील्ड में एक `useState` कॉल, दोनों करने से काम चल सकता है। जब आप इन दो चरम सीमाओं और समूह से संबंधित स्टेट के बीच कुछ इंडिपेंडेंट स्टेट वेरिएबल में संतुलन पाते हैं, तो कॉम्पोनेन्ट सबसे अधिक रीडबल होते हैं। यदि स्टेट लॉजिक जटिल हो जाता है, तो हम इसे [रिड्यूसर के साथ मैनेज](/docs/hooks-reference.html#usereducer) या कस्टम हुक के साथ मैनेज करने की सलाह देते हैं।

### क्या इफेक्ट को सिर्फ उपडटेस के बाद इस्तेमाल करना चाहिए? {#can-i-run-an-effect-only-on-updates}

यह एक दुर्लभ उपयोग मामला है। यदि आपको इसकी आवश्यकता है, तो आप मैन्युअल रूप से बूलियन मान को स्टोर करने के लिए एक [म्यूटेबल रेफ का उपयोग](#is-there-something-like-instance-variables) कर सकते हैं, चाहे आप पहले या बाद के रेंडर पर हों, फिर उस फ्लैग को अपने प्रभाव में देखें। (यदि आप खुद को अक्सर ऐसा करते हुए पाते हैं, तो आप इसके लिए एक कस्टम हुक बना सकते हैं।)

### पिछले प्रॉप्स या स्टेट को कैसे प्राप्त करें? {#how-to-get-the-previous-props-or-state}

वर्तमान में, आप इसे [रेफ के साथ](#is-there-something-like-instance-variables) मैन्युअल रूप से कर सकते हैं:

```js{6,8}
function Counter() {
  const [count, setCount] = useState(0);

  const prevCountRef = useRef();
  useEffect(() => {
    prevCountRef.current = count;
  });
  const prevCount = prevCountRef.current;

  return <h1>Now: {count}, before: {prevCount}</h1>;
}
```

यह थोड़ा जटिल हो सकता है लेकिन आप इसे कस्टम हुक में एक्सट्रेक्ट कर सकते हैं:

```js{3,7}
function Counter() {
  const [count, setCount] = useState(0);
  const prevCount = usePrevious(count);
  return <h1>Now: {count}, before: {prevCount}</h1>;
}

function usePrevious(value) {
  const ref = useRef();
  useEffect(() => {
    ref.current = value;
  });
  return ref.current;
}
```

ध्यान दें कि यह प्रॉप्स , स्टेट या किसी अन्य कैलक्युलेटेड वैल्यू के लिए कैसे काम करेगा.

```js{5}
function Counter() {
  const [count, setCount] = useState(0);

  const calculation = count + 100;
  const prevCalculation = usePrevious(calculation);
  // ...
```

It's possible that in the future React will provide a `usePrevious` Hook out of the box since it's a relatively common use case.

See also [the recommended pattern for derived state](#how-do-i-implement-getderivedstatefromprops).

### Why am I seeing stale props or state inside my function? {#why-am-i-seeing-stale-props-or-state-inside-my-function}

Any function inside a component, including event handlers and effects, "sees" the props and state from the render it was created in. For example, consider code like this:

```js
function Example() {
  const [count, setCount] = useState(0);

  function handleAlertClick() {
    setTimeout(() => {
      alert('You clicked on: ' + count);
    }, 3000);
  }

  return (
    <div>
      <p>You clicked {count} times</p>
      <button onClick={() => setCount(count + 1)}>
        Click me
      </button>
      <button onClick={handleAlertClick}>
        Show alert
      </button>
    </div>
  );
}
```

If you first click "Show alert" and then increment the counter, the alert will show the `count` variable **at the time you clicked the "Show alert" button**. This prevents bugs caused by the code assuming props and state don't change.

If you intentionally want to read the *latest* state from some asynchronous callback, you could keep it in [a ref](/docs/hooks-faq.html#is-there-something-like-instance-variables), mutate it, and read from it.

Finally, another possible reason you're seeing stale props or state is if you use the "dependency array" optimization but didn't correctly specify all the dependencies. For example, if an effect specifies `[]` as the second argument but reads `someProp` inside, it will keep "seeing" the initial value of `someProp`. The solution is to either remove the dependency array, or to fix it. Here's [how you can deal with functions](#is-it-safe-to-omit-functions-from-the-list-of-dependencies), and here's [other common strategies](#what-can-i-do-if-my-effect-dependencies-change-too-often) to run effects less often without incorrectly skipping dependencies.

>Note
>
>We provide an [`exhaustive-deps`](https://github.com/facebook/react/issues/14920) ESLint rule as a part of the [`eslint-plugin-react-hooks`](https://www.npmjs.com/package/eslint-plugin-react-hooks#installation) package. It warns when dependencies are specified incorrectly and suggests a fix.

### How do I implement `getDerivedStateFromProps`? {#how-do-i-implement-getderivedstatefromprops}

While you probably [don't need it](/blog/2018/06/07/you-probably-dont-need-derived-state.html), in rare cases that you do (such as implementing a `<Transition>` component), you can update the state right during rendering. React will re-run the component with updated state immediately after exiting the first render so it wouldn't be expensive.

Here, we store the previous value of the `row` prop in a state variable so that we can compare:

```js
function ScrollView({row}) {
  const [isScrollingDown, setIsScrollingDown] = useState(false);
  const [prevRow, setPrevRow] = useState(null);

  if (row !== prevRow) {
    // Row changed since last render. Update isScrollingDown.
    setIsScrollingDown(prevRow !== null && row > prevRow);
    setPrevRow(row);
  }

  return `Scrolling down: ${isScrollingDown}`;
}
```

This might look strange at first, but an update during rendering is exactly what `getDerivedStateFromProps` has always been like conceptually.

### Is there something like forceUpdate? {#is-there-something-like-forceupdate}

Both `useState` and `useReducer` Hooks [bail out of updates](/docs/hooks-reference.html#bailing-out-of-a-state-update) if the next value is the same as the previous one. Mutating state in place and calling `setState` will not cause a re-render.

Normally, you shouldn't mutate local state in React. However, as an escape hatch, you can use an incrementing counter to force a re-render even if the state has not changed:

```js
  const [ignored, forceUpdate] = useReducer(x => x + 1, 0);

  function handleClick() {
    forceUpdate();
  }
```

Try to avoid this pattern if possible.

### Can I make a ref to a function component? {#can-i-make-a-ref-to-a-function-component}

While you shouldn't need this often, you may expose some imperative methods to a parent component with the [`useImperativeHandle`](/docs/hooks-reference.html#useimperativehandle) Hook.

### How can I measure a DOM node? {#how-can-i-measure-a-dom-node}

One rudimentary way to measure the position or size of a DOM node is to use a [callback ref](/docs/refs-and-the-dom.html#callback-refs). React will call that callback whenever the ref gets attached to a different node. Here is a [small demo](https://codesandbox.io/s/l7m0v5x4v9):

```js{4-8,12}
function MeasureExample() {
  const [height, setHeight] = useState(0);

  const measuredRef = useCallback(node => {
    if (node !== null) {
      setHeight(node.getBoundingClientRect().height);
    }
  }, []);

  return (
    <>
      <h1 ref={measuredRef}>Hello, world</h1>
      <h2>The above header is {Math.round(height)}px tall</h2>
    </>
  );
}
```

We didn't choose `useRef` in this example because an object ref doesn't notify us about *changes* to the current ref value. Using a callback ref ensures that [even if a child component displays the measured node later](https://codesandbox.io/s/818zzk8m78) (e.g. in response to a click), we still get notified about it in the parent component and can update the measurements.

Note that we pass `[]` as a dependency array to `useCallback`. This ensures that our ref callback doesn't change between the re-renders, and so React won't call it unnecessarily.

In this example, the callback ref will be called only when the component mounts and unmounts, since the rendered `<h1>` component stays present throughout any rerenders. If you want to be notified any time a component resizes, you may want to use [`ResizeObserver`](https://developer.mozilla.org/en-US/docs/Web/API/ResizeObserver) or a third-party Hook built on it.

If you want, you can [extract this logic](https://codesandbox.io/s/m5o42082xy) into a reusable Hook:

```js{2}
function MeasureExample() {
  const [rect, ref] = useClientRect();
  return (
    <>
      <h1 ref={ref}>Hello, world</h1>
      {rect !== null &&
        <h2>The above header is {Math.round(rect.height)}px tall</h2>
      }
    </>
  );
}

function useClientRect() {
  const [rect, setRect] = useState(null);
  const ref = useCallback(node => {
    if (node !== null) {
      setRect(node.getBoundingClientRect());
    }
  }, []);
  return [rect, ref];
}
```


### What does `const [thing, setThing] = useState()` mean? {#what-does-const-thing-setthing--usestate-mean}

If you're not familiar with this syntax, check out the [explanation](/docs/hooks-state.html#tip-what-do-square-brackets-mean) in the State Hook documentation.


## Performance Optimizations {#performance-optimizations}

### Can I skip an effect on updates? {#can-i-skip-an-effect-on-updates}

Yes. See [conditionally firing an effect](/docs/hooks-reference.html#conditionally-firing-an-effect). Note that forgetting to handle updates often [introduces bugs](/docs/hooks-effect.html#explanation-why-effects-run-on-each-update), which is why this isn't the default behavior.

### Is it safe to omit functions from the list of dependencies? {#is-it-safe-to-omit-functions-from-the-list-of-dependencies}

Generally speaking, no.

```js{3,8}
function Example({ someProp }) {
  function doSomething() {
    console.log(someProp);
  }

  useEffect(() => {
    doSomething();
  }, []); // 🔴 This is not safe (it calls `doSomething` which uses `someProp`)
}
```

It's difficult to remember which props or state are used by functions outside of the effect. This is why **usually you'll want to declare functions needed by an effect *inside* of it.** Then it's easy to see what values from the component scope that effect depends on:

```js{4,8}
function Example({ someProp }) {
  useEffect(() => {
    function doSomething() {
      console.log(someProp);
    }

    doSomething();
  }, [someProp]); // ✅ OK (our effect only uses `someProp`)
}
```

If after that we still don't use any values from the component scope, it's safe to specify `[]`:

```js{7}
useEffect(() => {
  function doSomething() {
    console.log('hello');
  }

  doSomething();
}, []); // ✅ OK in this example because we don't use *any* values from component scope
```

Depending on your use case, there are a few more options described below.

>Note
>
>We provide the [`exhaustive-deps`](https://github.com/facebook/react/issues/14920) ESLint rule as a part of the [`eslint-plugin-react-hooks`](https://www.npmjs.com/package/eslint-plugin-react-hooks#installation) package. It helps you find components that don't handle updates consistently.

Let's see why this matters.

If you specify a [list of dependencies](/docs/hooks-reference.html#conditionally-firing-an-effect) as the last argument to `useEffect`, `useMemo`, `useCallback`, or `useImperativeHandle`, it must include all values that are used inside the callback and participate in the React data flow. That includes props, state, and anything derived from them.

It is **only** safe to omit a function from the dependency list if nothing in it (or the functions called by it) references props, state, or values derived from them. This example has a bug:

```js{5,12}
function ProductPage({ productId }) {
  const [product, setProduct] = useState(null);

  async function fetchProduct() {
    const response = await fetch('http://myapi/product/' + productId); // Uses productId prop
    const json = await response.json();
    setProduct(json);
  }

  useEffect(() => {
    fetchProduct();
  }, []); // 🔴 Invalid because `fetchProduct` uses `productId`
  // ...
}
```

**The recommended fix is to move that function _inside_ of your effect**. That makes it easy to see which props or state your effect uses, and to ensure they're all declared:

```js{5-10,13}
function ProductPage({ productId }) {
  const [product, setProduct] = useState(null);

  useEffect(() => {
    // By moving this function inside the effect, we can clearly see the values it uses.
    async function fetchProduct() {
      const response = await fetch('http://myapi/product/' + productId);
      const json = await response.json();
      setProduct(json);
    }

    fetchProduct();
  }, [productId]); // ✅ Valid because our effect only uses productId
  // ...
}
```

This also allows you to handle out-of-order responses with a local variable inside the effect:

```js{2,6,10}
  useEffect(() => {
    let ignore = false;
    async function fetchProduct() {
      const response = await fetch('http://myapi/product/' + productId);
      const json = await response.json();
      if (!ignore) setProduct(json);
    }

    fetchProduct();
    return () => { ignore = true };
  }, [productId]);
```

We moved the function inside the effect so it doesn't need to be in its dependency list.

>Tip
>
>Check out [this small demo](https://codesandbox.io/s/jvvkoo8pq3) and [this article](https://www.robinwieruch.de/react-hooks-fetch-data/) to learn more about data fetching with Hooks.

**If for some reason you _can't_ move a function inside an effect, there are a few more options:**

* **You can try moving that function outside of your component**. In that case, the function is guaranteed to not reference any props or state, and also doesn't need to be in the list of dependencies.
* If the function you're calling is a pure computation and is safe to call while rendering, you may **call it outside of the effect instead,** and make the effect depend on the returned value.
* As a last resort, you can **add a function to effect dependencies but _wrap its definition_** into the [`useCallback`](/docs/hooks-reference.html#usecallback) Hook. This ensures it doesn't change on every render unless *its own* dependencies also change:

```js{2-5}
function ProductPage({ productId }) {
  // ✅ Wrap with useCallback to avoid change on every render
  const fetchProduct = useCallback(() => {
    // ... Does something with productId ...
  }, [productId]); // ✅ All useCallback dependencies are specified

  return <ProductDetails fetchProduct={fetchProduct} />;
}

function ProductDetails({ fetchProduct }) {
  useEffect(() => {
    fetchProduct();
  }, [fetchProduct]); // ✅ All useEffect dependencies are specified
  // ...
}
```

Note that in the above example we **need** to keep the function in the dependencies list. This ensures that a change in the `productId` prop of `ProductPage` automatically triggers a refetch in the `ProductDetails` component.

### What can I do if my effect dependencies change too often? {#what-can-i-do-if-my-effect-dependencies-change-too-often}

Sometimes, your effect may be using state that changes too often. You might be tempted to omit that state from a list of dependencies, but that usually leads to bugs:

```js{6,9}
function Counter() {
  const [count, setCount] = useState(0);

  useEffect(() => {
    const id = setInterval(() => {
      setCount(count + 1); // This effect depends on the `count` state
    }, 1000);
    return () => clearInterval(id);
  }, []); // 🔴 Bug: `count` is not specified as a dependency

  return <h1>{count}</h1>;
}
```

The empty set of dependencies, `[]`, means that the effect will only run once when the component mounts, and not on every re-render. The problem is that inside the `setInterval` callback, the value of `count` does not change, because we've created a closure with the value of `count` set to `0` as it was when the effect callback ran. Every second, this callback then calls `setCount(0 + 1)`, so the count never goes above 1.

Specifying `[count]` as a list of dependencies would fix the bug, but would cause the interval to be reset on every change. Effectively, each `setInterval` would get one chance to execute before being cleared (similar to a `setTimeout`.) That may not be desirable. To fix this, we can use the [functional update form of `setState`](/docs/hooks-reference.html#functional-updates). It lets us specify *how* the state needs to change without referencing the *current* state:

```js{6,9}
function Counter() {
  const [count, setCount] = useState(0);

  useEffect(() => {
    const id = setInterval(() => {
      setCount(c => c + 1); // ✅ This doesn't depend on `count` variable outside
    }, 1000);
    return () => clearInterval(id);
  }, []); // ✅ Our effect doesn't use any variables in the component scope

  return <h1>{count}</h1>;
}
```

(The identity of the `setCount` function is guaranteed to be stable so it's safe to omit.)

Now, the `setInterval` callback executes once a second, but each time the inner call to `setCount` can use an up-to-date value for `count` (called `c` in the callback here.)

In more complex cases (such as if one state depends on another state), try moving the state update logic outside the effect with the [`useReducer` Hook](/docs/hooks-reference.html#usereducer). [This article](https://adamrackis.dev/state-and-use-reducer/) offers an example of how you can do this. **The identity of the `dispatch` function from `useReducer` is always stable** — even if the reducer function is declared inside the component and reads its props.

As a last resort, if you want something like `this` in a class, you can [use a ref](/docs/hooks-faq.html#is-there-something-like-instance-variables) to hold a mutable variable. Then you can write and read to it. For example:

```js{2-6,10-11,16}
function Example(props) {
  // Keep latest props in a ref.
  const latestProps = useRef(props);
  useEffect(() => {
    latestProps.current = props;
  });

  useEffect(() => {
    function tick() {
      // Read latest props at any time
      console.log(latestProps.current);
    }

    const id = setInterval(tick, 1000);
    return () => clearInterval(id);
  }, []); // This effect never re-runs
}
```

Only do this if you couldn't find a better alternative, as relying on mutation makes components less predictable. If there's a specific pattern that doesn't translate well, [file an issue](https://github.com/facebook/react/issues/new) with a runnable example code and we can try to help.

### How do I implement `shouldComponentUpdate`? {#how-do-i-implement-shouldcomponentupdate}

You can wrap a function component with `React.memo` to shallowly compare its props:

```js
const Button = React.memo((props) => {
  // your component
});
```

It's not a Hook because it doesn't compose like Hooks do. `React.memo` is equivalent to `PureComponent`, but it only compares props. (You can also add a second argument to specify a custom comparison function that takes the old and new props. If it returns true, the update is skipped.)

`React.memo` doesn't compare state because there is no single state object to compare. But you can make children pure too, or even [optimize individual children with `useMemo`](/docs/hooks-faq.html#how-to-memoize-calculations).

### How to memoize calculations? {#how-to-memoize-calculations}

The [`useMemo`](/docs/hooks-reference.html#usememo) Hook lets you cache calculations between multiple renders by "remembering" the previous computation:

```js
const memoizedValue = useMemo(() => computeExpensiveValue(a, b), [a, b]);
```

This code calls `computeExpensiveValue(a, b)`. But if the dependencies `[a, b]` haven't changed since the last value, `useMemo` skips calling it a second time and simply reuses the last value it returned.

Remember that the function passed to `useMemo` runs during rendering. Don't do anything there that you wouldn't normally do while rendering. For example, side effects belong in `useEffect`, not `useMemo`.

**You may rely on `useMemo` as a performance optimization, not as a semantic guarantee.** In the future, React may choose to "forget" some previously memoized values and recalculate them on next render, e.g. to free memory for offscreen components. Write your code so that it still works without `useMemo` — and then add it to optimize performance. (For rare cases when a value must *never* be recomputed, you can [lazily initialize](#how-to-create-expensive-objects-lazily) a ref.)

Conveniently, `useMemo` also lets you skip an expensive re-render of a child:

```js
function Parent({ a, b }) {
  // Only re-rendered if `a` changes:
  const child1 = useMemo(() => <Child1 a={a} />, [a]);
  // Only re-rendered if `b` changes:
  const child2 = useMemo(() => <Child2 b={b} />, [b]);
  return (
    <>
      {child1}
      {child2}
    </>
  )
}
```

Note that this approach won't work in a loop because Hook calls [can't](/docs/hooks-rules.html) be placed inside loops. But you can extract a separate component for the list item, and call `useMemo` there.

### How to create expensive objects lazily? {#how-to-create-expensive-objects-lazily}

`useMemo` lets you [memoize an expensive calculation](#how-to-memoize-calculations) if the dependencies are the same. However, it only serves as a hint, and doesn't *guarantee* the computation won't re-run. But sometimes you need to be sure an object is only created once.

**The first common use case is when creating the initial state is expensive:**

```js
function Table(props) {
  // ⚠️ createRows() is called on every render
  const [rows, setRows] = useState(createRows(props.count));
  // ...
}
```

To avoid re-creating the ignored initial state, we can pass a **function** to `useState`:

```js
function Table(props) {
  // ✅ createRows() is only called once
  const [rows, setRows] = useState(() => createRows(props.count));
  // ...
}
```

React will only call this function during the first render. See the [`useState` API reference](/docs/hooks-reference.html#usestate).

**You might also occasionally want to avoid re-creating the `useRef()` initial value.** For example, maybe you want to ensure some imperative class instance only gets created once:

```js
function Image(props) {
  // ⚠️ IntersectionObserver is created on every render
  const ref = useRef(new IntersectionObserver(onIntersect));
  // ...
}
```

`useRef` **does not** accept a special function overload like `useState`. Instead, you can write your own function that creates and sets it lazily:

```js
function Image(props) {
  const ref = useRef(null);

  // ✅ IntersectionObserver is created lazily once
  function getObserver() {
    if (ref.current === null) {
      ref.current = new IntersectionObserver(onIntersect);
    }
    return ref.current;
  }

  // When you need it, call getObserver()
  // ...
}
```

This avoids creating an expensive object until it's truly needed for the first time. If you use Flow or TypeScript, you can also give `getObserver()` a non-nullable type for convenience.


### Are Hooks slow because of creating functions in render? {#are-hooks-slow-because-of-creating-functions-in-render}

No. In modern browsers, the raw performance of closures compared to classes doesn't differ significantly except in extreme scenarios.

In addition, consider that the design of Hooks is more efficient in a couple ways:

* Hooks avoid a lot of the overhead that classes require, like the cost of creating class instances and binding event handlers in the constructor.

* **Idiomatic code using Hooks doesn't need the deep component tree nesting** that is prevalent in codebases that use higher-order components, render props, and context. With smaller component trees, React has less work to do.

Traditionally, performance concerns around inline functions in React have been related to how passing new callbacks on each render breaks `shouldComponentUpdate` optimizations in child components. Hooks approach this problem from three sides.

* The [`useCallback`](/docs/hooks-reference.html#usecallback) Hook lets you keep the same callback reference between re-renders so that `shouldComponentUpdate` continues to work:

    ```js{2}
    // Will not change unless `a` or `b` changes
    const memoizedCallback = useCallback(() => {
      doSomething(a, b);
    }, [a, b]);
    ```

* The [`useMemo`](/docs/hooks-faq.html#how-to-memoize-calculations) Hook makes it easier to control when individual children update, reducing the need for pure components.

* Finally, the [`useReducer`](/docs/hooks-reference.html#usereducer) Hook reduces the need to pass callbacks deeply, as explained below.

### How to avoid passing callbacks down? {#how-to-avoid-passing-callbacks-down}

We've found that most people don't enjoy manually passing callbacks through every level of a component tree. Even though it is more explicit, it can feel like a lot of "plumbing".

In large component trees, an alternative we recommend is to pass down a `dispatch` function from [`useReducer`](/docs/hooks-reference.html#usereducer) via context:

```js{4,5}
const TodosDispatch = React.createContext(null);

function TodosApp() {
  // Note: `dispatch` won't change between re-renders
  const [todos, dispatch] = useReducer(todosReducer);

  return (
    <TodosDispatch.Provider value={dispatch}>
      <DeepTree todos={todos} />
    </TodosDispatch.Provider>
  );
}
```

Any child in the tree inside `TodosApp` can use the `dispatch` function to pass actions up to `TodosApp`:

```js{2,3}
function DeepChild(props) {
  // If we want to perform an action, we can get dispatch from context.
  const dispatch = useContext(TodosDispatch);

  function handleClick() {
    dispatch({ type: 'add', text: 'hello' });
  }

  return (
    <button onClick={handleClick}>Add todo</button>
  );
}
```

This is both more convenient from the maintenance perspective (no need to keep forwarding callbacks), and avoids the callback problem altogether. Passing `dispatch` down like this is the recommended pattern for deep updates.

Note that you can still choose whether to pass the application *state* down as props (more explicit) or as context (more convenient for very deep updates). If you use context to pass down the state too, use two different context types -- the `dispatch` context never changes, so components that read it don't need to rerender unless they also need the application state.

### How to read an often-changing value from `useCallback`? {#how-to-read-an-often-changing-value-from-usecallback}

>Note
>
>We recommend to [pass `dispatch` down in context](#how-to-avoid-passing-callbacks-down) rather than individual callbacks in props. The approach below is only mentioned here for completeness and as an escape hatch.
>
>Also note that this pattern might cause problems in the [concurrent mode](/blog/2018/03/27/update-on-async-rendering.html). We plan to provide more ergonomic alternatives in the future, but the safest solution right now is to always invalidate the callback if some value it depends on changes.

In some rare cases you might need to memoize a callback with [`useCallback`](/docs/hooks-reference.html#usecallback) but the memoization doesn't work very well because the inner function has to be re-created too often. If the function you're memoizing is an event handler and isn't used during rendering, you can use [ref as an instance variable](#is-there-something-like-instance-variables), and save the last committed value into it manually:

```js{6,10}
function Form() {
  const [text, updateText] = useState('');
  const textRef = useRef();

  useEffect(() => {
    textRef.current = text; // Write it to the ref
  });

  const handleSubmit = useCallback(() => {
    const currentText = textRef.current; // Read it from the ref
    alert(currentText);
  }, [textRef]); // Don't recreate handleSubmit like [text] would do

  return (
    <>
      <input value={text} onChange={e => updateText(e.target.value)} />
      <ExpensiveTree onSubmit={handleSubmit} />
    </>
  );
}
```

This is a rather convoluted pattern but it shows that you can do this escape hatch optimization if you need it. It's more bearable if you extract it to a custom Hook:

```js{4,16}
function Form() {
  const [text, updateText] = useState('');
  // Will be memoized even if `text` changes:
  const handleSubmit = useEventCallback(() => {
    alert(text);
  }, [text]);

  return (
    <>
      <input value={text} onChange={e => updateText(e.target.value)} />
      <ExpensiveTree onSubmit={handleSubmit} />
    </>
  );
}

function useEventCallback(fn, dependencies) {
  const ref = useRef(() => {
    throw new Error('Cannot call an event handler while rendering.');
  });

  useEffect(() => {
    ref.current = fn;
  }, [fn, ...dependencies]);

  return useCallback(() => {
    const fn = ref.current;
    return fn();
  }, [ref]);
}
```

In either case, we **don't recommend this pattern** and only show it here for completeness. Instead, it is preferable to [avoid passing callbacks deep down](#how-to-avoid-passing-callbacks-down).


## Under the Hood {#under-the-hood}

### How does React associate Hook calls with components? {#how-does-react-associate-hook-calls-with-components}

React keeps track of the currently rendering component. Thanks to the [Rules of Hooks](/docs/hooks-rules.html), we know that Hooks are only called from React components (or custom Hooks -- which are also only called from React components).

There is an internal list of "memory cells" associated with each component. They're just JavaScript objects where we can put some data. When you call a Hook like `useState()`, it reads the current cell (or initializes it during the first render), and then moves the pointer to the next one. This is how multiple `useState()` calls each get independent local state.

### What is the prior art for Hooks? {#what-is-the-prior-art-for-hooks}

Hooks synthesize ideas from several different sources:

* Our old experiments with functional APIs in the [react-future](https://github.com/reactjs/react-future/tree/master/07%20-%20Returning%20State) repository.
* React community's experiments with render prop APIs, including [Ryan Florence](https://github.com/ryanflorence)'s [Reactions Component](https://github.com/reactions/component).
* [Dominic Gannaway](https://github.com/trueadm)'s [`adopt` keyword](https://gist.github.com/trueadm/17beb64288e30192f3aa29cad0218067) proposal as a sugar syntax for render props.
* State variables and state cells in [DisplayScript](http://displayscript.org/introduction.html).
* [Reducer components](https://reasonml.github.io/reason-react/docs/en/state-actions-reducer.html) in ReasonReact.
* [Subscriptions](http://reactivex.io/rxjs/class/es6/Subscription.js~Subscription.html) in Rx.
* [Algebraic effects](https://github.com/ocamllabs/ocaml-effects-tutorial#2-effectful-computations-in-a-pure-setting) in Multicore OCaml.

[Sebastian Markbåge](https://github.com/sebmarkbage) came up with the original design for Hooks, later refined by [Andrew Clark](https://github.com/acdlite), [Sophie Alpert](https://github.com/sophiebits), [Dominic Gannaway](https://github.com/trueadm), and other members of the React team.
