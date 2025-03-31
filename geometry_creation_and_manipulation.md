# Geometry Creation and Manipulation in Three.js

## Introduction

Three.js provides a powerful set of tools for creating and manipulating 3D geometries. This guide will walk you through the process of working with built-in geometry types, creating custom geometries, and modifying geometries at runtime.

## Built-in Geometry Types

Three.js offers several built-in geometry types that you can use out of the box. One of the most common is the `BoxGeometry`. Let's look at how to create a simple cube using `BoxGeometry`:

```javascript
const geometry = new THREE.BoxGeometry(1, 1, 1);
const material = new THREE.MeshBasicMaterial({ color: 0x00ff00 });
const cube = new THREE.Mesh(geometry, material);
scene.add(cube);
```

In this example, we create a cube with dimensions of 1x1x1 units. The `BoxGeometry` constructor accepts parameters for width, height, and depth, as well as the number of segments for each dimension:

```javascript
const geometry = new THREE.BoxGeometry(width, height, depth, widthSegments, heightSegments, depthSegments);
```

## Creating Custom Geometries

For more complex shapes, you may need to create custom geometries. Three.js provides the `BufferGeometry` class for this purpose. Here's an example of creating a custom triangle:

```javascript
const geometry = new THREE.BufferGeometry();
const vertices = new Float32Array([
    -1.0, -1.0,  1.0,
     1.0, -1.0,  1.0,
     1.0,  1.0,  1.0,
]);

geometry.setAttribute('position', new THREE.BufferAttribute(vertices, 3));
const material = new THREE.MeshBasicMaterial({ color: 0xff0000 });
const triangle = new THREE.Mesh(geometry, material);
scene.add(triangle);
```

In this example, we:
1. Create a new `BufferGeometry` instance.
2. Define an array of vertex positions.
3. Set the 'position' attribute of the geometry using `setAttribute`.
4. Create a mesh using the custom geometry and add it to the scene.

## Manipulating Geometries at Runtime

Three.js allows you to modify geometries dynamically. Here are some techniques:

### Modifying Vertex Positions

You can change vertex positions by accessing the position attribute:

```javascript
const positionAttribute = geometry.getAttribute('position');
positionAttribute.setXYZ(index, x, y, z);
positionAttribute.needsUpdate = true;
```

### Adding New Attributes

You can add custom attributes to your geometry:

```javascript
const colors = new Float32Array([
    1.0, 0.0, 0.0,
    0.0, 1.0, 0.0,
    0.0, 0.0, 1.0
]);
geometry.setAttribute('color', new THREE.BufferAttribute(colors, 3));
```

### Compute Vertex Normals

If you've modified your geometry, you might need to recompute normals:

```javascript
geometry.computeVertexNormals();
```

## Advanced Techniques

### Merging Geometries

You can combine multiple geometries into one:

```javascript
const geometryA = new THREE.BoxGeometry(1, 1, 1);
const geometryB = new THREE.SphereGeometry(0.5, 32, 32);
geometryB.translate(1, 0, 0);

const mergedGeometry = BufferGeometryUtils.mergeBufferGeometries([geometryA, geometryB]);
const material = new THREE.MeshBasicMaterial({ color: 0xffff00 });
const mergedMesh = new THREE.Mesh(mergedGeometry, material);
scene.add(mergedMesh);
```

### Creating Indexed Geometries

Indexed geometries can be more efficient for complex shapes:

```javascript
const geometry = new THREE.BufferGeometry();

const vertices = new Float32Array([
    -1.0, -1.0,  1.0,
     1.0, -1.0,  1.0,
     1.0,  1.0,  1.0,
    -1.0,  1.0,  1.0,
]);

const indices = new Uint16Array([
    0, 1, 2,
    2, 3, 0
]);

geometry.setAttribute('position', new THREE.BufferAttribute(vertices, 3));
geometry.setIndex(new THREE.BufferAttribute(indices, 1));
```

## Conclusion

This guide has covered the basics of creating and manipulating geometries in Three.js. From using built-in geometries like `BoxGeometry` to creating custom shapes with `BufferGeometry`, you now have the tools to create complex 3D scenes. Remember to explore the Three.js documentation for more advanced features and optimizations.