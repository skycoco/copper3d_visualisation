# copper3d_visualisation

[![NPM Package][npm]][npm-url]

A 3d visualisation package base on threejs provides multiple scenes and Nrrd image load funtion.

### Documentation:

https://copper3d-visualisation.readthedocs.io/en/latest/

### Previous versions

see: https://www.npmjs.com/package/gltfloader-plugin-test

### Example

[Pick model with Gltfloader](https://linkungao.github.io/loadHumanModel_example/)

[Copper3d_examples](https://linkungao.github.io/copper3d_examples)

### Useage

- Load demo

```ts
import * as Copper from "copper3d_visualisation";
import { getCurrentInstance, onMounted } from "vue";
let refs = null;
let appRenderer;
onMounted(() => {
  let { $refs } = (getCurrentInstance() as any).proxy;
  refs = $refs;
  const bg: HTMLDivElement = refs.classfy;
  appRenderer = new Copper.copperRenderer(bg);
  const scene = appRenderer.getCurrentScene();
  scene.createDemoMesh();
  appRenderer.animate();
});
```

- Add options (curently only control gui)

```ts
appRenderer = new Copper.copperRenderer(bg, { guiOpen: true });
```

- Load multiple scenes with gltf-loader

```ts
import * as Copper from "copper3d_visualisation";
import { getCurrentInstance, onMounted } from "vue";

let refs = null;
let appRenderer;
onMounted(() => {
  let { $refs } = (getCurrentInstance() as any).proxy;
  refs = $refs;
  const bg: HTMLDivElement = refs.classfy;
  appRenderer = new Copper.copperRenderer(bg);
  appRenderer.animate();
  loadModel("/Healthy.glb", "health");
});

function loadModel(url, name) {
  let scene1 = appRenderer.getSceneByName(name);
  if (scene1 == undefined) {
    const scene1 = appRenderer.createScene(name);
    appRenderer.setCurrentScene(scene1);
    scene1.loadViewUrl("/noInfarct_view.json");
    scene1.loadGltf(url);
  } else {
    appRenderer.setCurrentScene(scene1);
  }
}
```

#### Viewdata Structure

```ts
 CameraViewPoint {
  nearPlane: number = 0.1;
  farPlane: number = 2000.0;
  eyePosition: Array<number> = [0.0, 0.0, 0.0];
  targetPosition: Array<number> = [0.0, 0.0, 0.0];
  upVector: Array<number> = [0.0, 1.0, 0.0];
}
```
