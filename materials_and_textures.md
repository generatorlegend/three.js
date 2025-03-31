# Materials and Textures in Three.js

## Introduction

Materials and textures are essential components in Three.js that define the appearance of 3D objects in your scene. This guide will walk you through the process of working with materials and textures, explaining different types of materials, how to apply textures, and how to create realistic-looking surfaces.

## Materials

Materials in Three.js determine how objects interact with light and appear in the scene. There are several types of materials available, each with its own properties and use cases.

### MeshStandardMaterial

The `MeshStandardMaterial` is a physically based material that provides a more realistic rendering compared to simpler materials like `MeshBasicMaterial` or `MeshLambertMaterial`. It uses the Metallic-Roughness workflow, which is common in modern 3D applications.

Here's an example of how to create and use a `MeshStandardMaterial`:

```javascript
const material = new THREE.MeshStandardMaterial({
  color: 0x00ff00,     // Base color of the material
  roughness: 0.5,      // How rough the material appears
  metalness: 0.5,      // How metallic the material appears
});

const cube = new THREE.Mesh(new THREE.BoxGeometry(), material);
scene.add(cube);
```

Key properties of `MeshStandardMaterial`:

- `color`: The base color of the material
- `roughness`: Defines how rough the material appears (0 for smooth, 1 for rough)
- `metalness`: Defines how metallic the material appears (0 for non-metallic, 1 for metallic)
- `map`: The color texture
- `normalMap`: The normal map texture for simulating surface details
- `roughnessMap`: The roughness map texture
- `metalnessMap`: The metalness map texture

## Textures

Textures are images that can be applied to materials to add detail and realism to 3D objects. They can represent color, roughness, normal maps, and more.

### Loading Textures

To load a texture, you can use the `TextureLoader`:

```javascript
const textureLoader = new THREE.TextureLoader();
const colorTexture = textureLoader.load('path/to/color_texture.jpg');
const normalTexture = textureLoader.load('path/to/normal_texture.jpg');
const roughnessTexture = textureLoader.load('path/to/roughness_texture.jpg');

const material = new THREE.MeshStandardMaterial({
  map: colorTexture,
  normalMap: normalTexture,
  roughnessMap: roughnessTexture,
});
```

### Texture Properties

Textures have several properties that control how they are applied to materials:

- `wrapS` and `wrapT`: Define how the texture wraps horizontally and vertically
- `repeat`: Controls how many times the texture is repeated
- `offset`: Moves the texture's position
- `rotation`: Rotates the texture

Example of adjusting texture properties:

```javascript
const texture = textureLoader.load('texture.jpg');
texture.wrapS = THREE.RepeatWrapping;
texture.wrapT = THREE.RepeatWrapping;
texture.repeat.set(2, 2);
texture.offset.set(0.5, 0.5);
texture.rotation = Math.PI / 4;
```

## Creating Realistic Surfaces

To create realistic-looking surfaces, combine different texture maps and adjust material properties:

1. Use a color map for base color information
2. Apply a normal map to add surface details without increasing geometry complexity
3. Use a roughness map to control the microscale roughness of the surface
4. For metallic objects, use a metalness map to define which parts are metallic and which are not

Example of a realistic material setup:

```javascript
const material = new THREE.MeshStandardMaterial({
  map: textureLoader.load('color.jpg'),
  normalMap: textureLoader.load('normal.jpg'),
  roughnessMap: textureLoader.load('roughness.jpg'),
  metalnessMap: textureLoader.load('metalness.jpg'),
  roughness: 0.5,
  metalness: 0.5,
});
```

## Conclusion

Understanding materials and textures is crucial for creating visually appealing 3D scenes in Three.js. Experiment with different material types, texture combinations, and property adjustments to achieve the desired look for your objects. Remember that while `MeshStandardMaterial` provides realistic results, it's also more computationally expensive than simpler materials, so choose the appropriate material based on your project's requirements and performance constraints.