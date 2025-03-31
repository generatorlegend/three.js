# Animation Basics in Three.js

Three.js provides powerful tools for creating animations in your 3D scenes. This guide will introduce you to the basics of animation in Three.js, covering how to animate object properties, use the AnimationMixer for keyframe animations, and create simple interactive animations using user input.

## Animating Object Properties

The simplest way to create animations in Three.js is by modifying object properties over time. This can be done in your render loop or using requestAnimationFrame.

### Example: Rotating a Cube

```javascript
const cube = new THREE.Mesh(
  new THREE.BoxGeometry(1, 1, 1),
  new THREE.MeshBasicMaterial({ color: 0x00ff00 })
);
scene.add(cube);

function animate() {
  requestAnimationFrame(animate);

  // Rotate the cube
  cube.rotation.x += 0.01;
  cube.rotation.y += 0.01;

  renderer.render(scene, camera);
}

animate();
```

In this example, we're incrementing the rotation of the cube on each frame, creating a simple rotation animation.

## Using AnimationMixer for Keyframe Animations

For more complex animations, especially those created in 3D modeling software, Three.js provides the AnimationMixer class. This allows you to play and blend keyframe animations.

### Example: Playing a Keyframe Animation

```javascript
import { AnimationMixer } from 'three';

let mixer, clock;

// Assume 'model' is a loaded 3D model with animations
function initAnimation(model) {
  mixer = new AnimationMixer(model);
  const clip = model.animations[0]; // Get the first animation clip
  const action = mixer.clipAction(clip);
  action.play();

  clock = new THREE.Clock();
}

function animate() {
  requestAnimationFrame(animate);

  if (mixer) {
    const delta = clock.getDelta();
    mixer.update(delta);
  }

  renderer.render(scene, camera);
}

animate();
```

In this example, we create an AnimationMixer for our model, play the first animation clip, and update the mixer on each frame.

## Creating Interactive Animations

You can also create animations that respond to user input. Here's an example of how to make an object move based on keyboard input:

```javascript
const speed = 0.1;
const object = new THREE.Mesh(
  new THREE.SphereGeometry(0.5, 32, 32),
  new THREE.MeshBasicMaterial({ color: 0xff0000 })
);
scene.add(object);

document.addEventListener('keydown', onKeyDown);

function onKeyDown(event) {
  switch (event.keyCode) {
    case 37: // Left arrow
      object.position.x -= speed;
      break;
    case 39: // Right arrow
      object.position.x += speed;
      break;
    case 38: // Up arrow
      object.position.y += speed;
      break;
    case 40: // Down arrow
      object.position.y -= speed;
      break;
  }
}

function animate() {
  requestAnimationFrame(animate);
  renderer.render(scene, camera);
}

animate();
```

This code moves the object left, right, up, or down based on arrow key presses.

## Conclusion

These examples cover the basics of animation in Three.js. Remember that the key to smooth animations is to update your scene in the animation loop and to keep your animations performance-efficient. As you become more comfortable with these concepts, you can create more complex and engaging animations in your Three.js projects.

For more advanced animation techniques, refer to the Three.js documentation on AnimationMixer and AnimationClip classes.