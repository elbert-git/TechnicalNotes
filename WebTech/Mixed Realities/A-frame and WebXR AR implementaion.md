# **A-frame and AR Markerless implementaion**

===================================================================

### in General

A markerless web AR implementation used in the hatten CNY AR greeting card

### limitations

Usual webGL restrictions apply. But the biggest one is Apple. WebXR don't work on iphones. Best to use their own reality viewer to let apple users exprience the same AR model.

### Setup HTML

* Import this version of a-frame

```
<script src="https://aframe.io/releases/1.2.0/aframe.min.js"></script>
```

* Import A-frame AR component

```
<script src="https://ada.is/basketball-demo/ar-components.js"></script>
```

* Setup a-frame scene

```
<a-scene 
 embedded
 webxr="optionalFeatures: hit-test, dom-overlay; overlayElement:#overlay;"
 vr-mode-ui="vrEnabled:false; arEnabled: true"
 background="transparent:true"
>
  <!--All your a-frame stuff goes inside.-->
<a-scene/>
```

* Create a-entity to be the main anchor point when you tap the model

```
<a-entity id="world">
  <!--AR content goes here-->
<a-entity/>
```

* create a-entity for the reticle

```
<a-entity ar-hit-test="target:{id of main content a-entity}">
  <!--reticle model goes here-->
</a-entity>
```

---

---

---

# Important note ❗❗❗

Seems like the ar-hit-test component is now in the official a-frame library in version 1.3.0