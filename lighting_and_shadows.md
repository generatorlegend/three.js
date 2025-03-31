# Lighting and Shadows in Three.js

Three.js provides powerful capabilities for creating realistic lighting and shadows in your 3D scenes. This guide will walk you through the different types of lights available, how to create and position them, and how to enable and configure shadows for more immersive rendering.

## Types of Lights

Three.js offers several types of lights to illuminate your scenes:

1. AmbientLight
2. DirectionalLight
3. PointLight
4. SpotLight
5. HemisphereLight
6. RectAreaLight

Let's explore each type in detail.

### AmbientLight

AmbientLight illuminates all objects in the scene equally, without casting shadows. It's useful for providing a base level of illumination.

```javascript
const ambientLight = new THREE.AmbientLight(0xffffff, 0.5);
scene.add(ambientLight);
```

### DirectionalLight

DirectionalLight simulates light coming from a distant source, like the sun. All light rays are parallel and cast shadows.

```javascript
const directionalLight = new THREE.DirectionalLight(0xffffff, 1);
directionalLight.position.set(5, 5, 5);
scene.add(directionalLight);
```

### PointLight

PointLight emits light in all directions from a single point, similar to a light bulb. It can cast shadows.

```javascript
const pointLight = new THREE.PointLight(0xff0000, 1, 100);
pointLight.position.set(10, 10, 10);
scene.add(pointLight);
```

### SpotLight

SpotLight emits light in a cone shape from a single point. It's useful for creating focused lighting effects and can cast shadows.

```javascript
const spotLight = new THREE.SpotLight(0xffffff);
spotLight.position.set(100, 1000, 100);
spotLight.angle = Math.PI / 4;
spotLight.penumbra = 0.05;
spotLight.decay = 2;
spotLight.distance = 200;
scene.add(spotLight);
```

### HemisphereLight

HemisphereLight simulates sky and ground lighting. It doesn't cast shadows but provides a natural-looking illumination.

```javascript
const hemisphereLight = new THREE.HemisphereLight(0xffffbb, 0x080820, 1);
scene.add(hemisphereLight);
```

### RectAreaLight

RectAreaLight emits light uniformly across a rectangular plane. It's great for simulating light from windows or panel lights.

```javascript
const rectAreaLight = new THREE.RectAreaLight(0xffffff, 5, 4, 10);
rectAreaLight.position.set(5, 5, 0);
rectAreaLight.lookAt(0, 0, 0);
scene.add(rectAreaLight);
```

## Positioning Lights

When positioning lights, consider the following:

1. Use the `position.set(x, y, z)` method to place lights in your scene.
2. For directional lights, use `light.target` to set the direction.
3. Experiment with different positions to achieve the desired lighting effect.

## Enabling Shadows

To enable shadows in Three.js:

1. Set `renderer.shadowMap.enabled = true` on your WebGLRenderer.
2. For each light that should cast shadows, set `light.castShadow = true`.
3. For each object that should cast or receive shadows, set `object.castShadow = true` or `object.receiveShadow = true` respectively.

```javascript
// Enable shadows on the renderer
renderer.shadowMap.enabled = true;
renderer.shadowMap.type = THREE.PCFSoftShadowMap; // Optional: for softer shadows

// Configure lights to cast shadows
directionalLight.castShadow = true;
spotLight.castShadow = true;

// Configure objects to cast and receive shadows
const cube = new THREE.Mesh(new THREE.BoxGeometry(), new THREE.MeshPhongMaterial());
cube.castShadow = true;

const plane = new THREE.Mesh(new THREE.PlaneGeometry(20, 20), new THREE.MeshPhongMaterial());
plane.receiveShadow = true;
```

## Configuring Shadow Maps

To improve shadow quality and performance:

1. Adjust the shadow map size:
   ```javascript
   light.shadow.mapSize.width = 1024;
   light.shadow.mapSize.height = 1024;
   ```

2. Set the shadow camera frustum for directional and spot lights:
   ```javascript
   directionalLight.shadow.camera.near = 1;
   directionalLight.shadow.camera.far = 6;
   directionalLight.shadow.camera.top = 2;
   directionalLight.shadow.camera.right = 2;
   directionalLight.shadow.camera.bottom = -2;
   directionalLight.shadow.camera.left = -2;
   ```

3. Adjust the shadow bias to reduce shadow acne:
   ```javascript
   light.shadow.bias = -0.0005;
   ```

## Performance Considerations

1. Use shadow-casting lights sparingly, as they can be computationally expensive.
2. Consider using baked shadows or normal maps for static scenes.
3. Experiment with different shadow map sizes to balance quality and performance.
4. Use `PCFSoftShadowMap` for better quality shadows, but be aware of the performance impact.

## Conclusion

Proper lighting and shadows are crucial for creating realistic and immersive 3D scenes. Experiment with different light types, positions, and shadow settings to achieve the desired look for your Three.js projects. Remember to balance visual quality with performance, especially for complex scenes or applications targeting mobile devices.

For more detailed information on specific light types and their properties, refer to the Three.js documentation for each light class.