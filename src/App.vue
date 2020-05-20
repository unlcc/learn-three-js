<template>
  <div id="app">
    <div id="container"></div>
    <div>
      hahahahhaa
    </div>
  </div>
</template>

<script>
import * as Three from 'three';
export default {
  name: 'App',
  data () {
    return {
      camera: null,
      scene: null,
      renderer: null,
      mesh: null
    };
  },
  mounted () {
    let timer = null;
    window.onresize = () => {
      if (timer) {
        clearTimeout(timer);
      }
      timer = setTimeout(() => {
        this.init();
        this.animate();
      }, 500);
    };
    this.init();
    this.animate();
  },
  methods: {
    init () {
      let container = document.getElementById('container');
      this.camera = new Three.PerspectiveCamera(75, container.clientWidth / container.clientHeight, 0.01, 10);
      this.camera.position.z = 1;

      this.scene = new Three.Scene();

      let geometry = new Three.BoxGeometry(0.5, 0.3, 0.4);
      let material = new Three.MeshNormalMaterial({ color: 0x00ff00 });

      this.mesh = new Three.Mesh(geometry, material);
      this.scene.add(this.mesh);

      this.renderer = new Three.WebGLRenderer({antialias: true});
      this.renderer.setSize(container.clientWidth, container.clientHeight);
      container.appendChild(this.renderer.domElement);
    },
    animate () {
      requestAnimationFrame(this.animate);
      this.mesh.rotation.x += 0.1;
      this.mesh.rotation.y += 0.02;
      this.renderer.render(this.scene, this.camera);
    }
  }
};
</script>

<style>
* {
  margin: 0;
  padding: 0;
}
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #fff;
  position: relative;

}
#container {
  position: fixed;
  left: 0;
  top: 0;
  right: 0;
  bottom: 0;
  z-index: -1;
}
canvas { width: 100%; height: 100% }
</style>
