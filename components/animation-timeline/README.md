## aframe-animation-timeline-component

[animation]: https://github.com/supermedium/superframe/tree/master/components/animation

A modified timeline component by AfterNow for A-Frame to use with the [animation
component][animation] for declaratively defining and orchestrating timelines of
animations. The animation timeline component depends on the animation
component. Make sure to include that.

[Visit the original repo for basic usage and installation](https://github.com/supermedium/superframe/tree/master/components/animation)

Additional feature is having the ability to mix the timeline animation with model animations. This requires [aframe-extras](https://github.com/donmccurdy/aframe-extras) to use the `animation-mixer` component.

### How to use
Add a `<a-timeline-model-animation>` element in a `<a-timeline-group>` or individually inside `<a-assets>`. This component can use attributes such as `id`, `select`, and `duration`. The `id` (required) should be a unique id for this animation, whereas `select`(required) is a selector for the actual `<a-entity>` model. `duration`(not required) is used to set the duration of the animation, [see how to use](https://github.com/donmccurdy/aframe-extras).

This is the base example of the animation-timeline-component with a built in animation in the first `a-timeline-group`.

### Example

```html
<a-scene animation-timeline__1="timeline: #myTimeline;">
        <a-assets timeout="10000">
            <a-asset-item src="https://cdn.aframe.io/fonts/Roboto-msdf.json"></a-asset-item>

            <a-timeline id="myTimeline">
                <a-timeline-animation select="#text1" name="togglevisible"></a-timeline-animation>
                <a-timeline-animation select="#text1" name="fadein"></a-timeline-animation>
                <a-timeline-animation select="#text1" name="fadeout"></a-timeline-animation>
                <a-timeline-animation select="#text1" name="togglevisibleoff"></a-timeline-animation>

                <a-timeline-group>
                    <a-timeline-model-animation id="anim1" duration="1000" select="#samba"></a-timeline-model-animation>
                    <a-timeline-animation select="a-entity[mixin~=box]" name="fadein"></a-timeline-animation>
                    <a-timeline-animation select="a-entity[mixin~=box]" name="scale"></a-timeline-animation>
                    <a-timeline-animation select="a-entity[mixin~=box]" name="color"></a-timeline-animation>
                </a-timeline-group>

                <a-timeline-group>
                    <a-timeline-animation select="#text2" name="togglevisible"></a-timeline-animation>
                    <a-timeline-animation select="#text2" name="fadein"></a-timeline-animation>
                    <a-timeline-animation select="#text2" name="textcolor"></a-timeline-animation>
                </a-timeline-group>

                <a-timeline-animation select="#text2" name="fadeout"></a-timeline-animation>
                <a-timeline-animation select="#text2" name="togglevisibleoff"></a-timeline-animation>

                <a-timeline-animation select="#text3" name="togglevisible"></a-timeline-animation>
                <a-timeline-group>
                    <a-timeline-animation select="a-entity[mixin~=box]" name="color"></a-timeline-animation>
                    <a-timeline-animation select="a-entity[mixin~=box]" name="rotate"></a-timeline-animation>
                    <a-timeline-animation select="a-entity[mixin~=box]" name="position"></a-timeline-animation>
                    <a-timeline-animation select="#text3" name="fadein"></a-timeline-animation>
                    <a-timeline-animation select="#text3" name="positionin"></a-timeline-animation>
                </a-timeline-group>

                <a-timeline-animation select="#text3" name="positionout"></a-timeline-animation>
                <a-timeline-animation select="#text3" name="togglevisibleoff"></a-timeline-animation>

                <a-timeline-animation select="#text4" name="togglevisible"></a-timeline-animation>

                <a-timeline-group>
                    <a-timeline-animation select="#sky" name="color"></a-timeline-animation>
                    <a-timeline-animation select="#text4" name="fadein"></a-timeline-animation>
                </a-timeline-group>

                <a-timeline-animation select="#text4" name="fadeout" offset="500"></a-timeline-animation>
            </a-timeline>

            <a-mixin id="box"
            geometry="primitive: box"
            material="color: #AAA; opacity: 0"
            animation__fadein="property: material.opacity; dur: 2000; from: 0; to: 1; autoplay: false"
            animation__scale="property: scale; to: 2 20 2; dur: 2000; easing: easeInOutElastic; autoplay: false"
            animation__position="property: position; to: 0 30 -3; dur: 2000; autoplay: false"
            animation__color="property: material.color; from: #AAA; to: #222; dur: 2500; autoplay: false"
            animation__rotate="property: rotation; to: 0 360; dur: 1000; easing: easeInQuad; autoplay: false"
            scale="0.0001 0.0001 0.0001"
            ></a-mixin>

            <a-mixin id="text"
            text="align: center; color: #333; width: 6; opacity: 0"
            animation__fadein="property: text.opacity; from: 0; to: 1; dur: 3000; easing: linear; autoplay: false"
            animation__fadeout="property: text.opacity; from: 1; to: 0; dur: 3000; easing: linear; autoplay: false"
            animation__togglevisible="property: visible; from: false; to: true; dur: 1; autoplay: false"
            animation__togglevisibleoff="property: visible; from: true; to: false; dur: 1; autoplay: false"
            position="0 2 -3"
            visible="false"></a-mixin>
        </a-assets>

        <a-entity id="text1" mixin="text" text="value: Is this real life?"></a-entity>
        <a-entity id="text2" mixin="text" text="value: Is this just fantasy?; opacity: 0"
        animation__textcolor="property: text.color; from: #FAFAFA; to: #8C200E; dur: 2500; autoplay: false"></a-entity>
        <a-entity id="text3" mixin="text" text="value: Caught in a landslide." position="0 -10 0"
        animation__positionin="property: position; to: 0 2 -3; dur: 2500; autoplay: false"
        animation__positionout="property: position; from: 0 2 -3; to: -10 2 -3; dur: 3500; autoplay: false"></a-entity>
        <a-entity id="text4" mixin="text" text="value: No escape from reality."></a-entity>

        <a-entity position="0 -0.5 -10">
            <a-entity id="box1" mixin="box" position="-4 0 0"></a-entity>
            <a-entity mixin="box"></a-entity>
            <a-entity mixin="box" position="4 0 0"></a-entity>
        </a-entity>
        <a-entity
            id="samba"
            fbx-model="src: url(./assets/samba.fbx)"
            position="0 0 -2"
            scale="0.01 0.01 0.01"
            >
        </a-entity>

    <a-sky id="sky" color="#FAFAFA" animation__color="property: material.color; from: #FAFAFA; to: #111; dur: 2000; autoplay: false"></a-sky>
</a-scene>

```

### Caveats
* `a-timeline-animation` has an issue where `startEvents` doesn't work properly after the first time, therefore this only works for single run-throughs or looping ones.
