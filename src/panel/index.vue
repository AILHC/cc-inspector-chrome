<template>
  <div class="panel ccui-scrollbar">
    <vue-particles id="tsparticles" :options="options"></vue-particles>
    <div class="head">
      <img class="icon" src="../../doc/icon128.png" />
      <span class="txt">Cocos Inspector</span>
      <div style="flex: 1"></div>
      <!-- <a href="https://hits.seeyoufarm.com"> <img src="https://hits.seeyoufarm.com/api/count/incr/badge.svg?url=https%3A%2F%2Ftidys.github.io%2Fcc-inspector-chrome%2F&count_bg=%2379C83D&title_bg=%23555555&icon=codesandbox.svg&icon_color=%23E7E7E7&title=%E8%AE%BF%E9%97%AE%E6%AC%A1%E6%95%B0&edge_flat=false" /></a> -->
      <img src="https://api.visitorbadge.io/api/combined?path=cc-inspector-pages&countColor=%23d9e3f0&style=flat&labelStyle=none" />
    </div>
    <div class="content" :class="horizontal ? 'content-row' : 'content-col'">
      <div class="title">
        <p style="font-size: 40px; font-weight: bold; color: white">为Coocs游戏开发加速。</p>
        <div style="font-size: 18px; font-weight: normal; margin: 30px 0; line-height: 40px; color: white">
          在浏览器中查看节点树、节点属性。<br />支持Creator所有版本。<br />
          <a href="https://juejin.cn/post/7463836172559024179" target="_blank">详细功能介绍</a>
        </div>
        <div class="link">
          <CCButton color="rgb(38,187,255)" class="download" @click="onClickChrome">
            <div class="list">
              <img src="./res/chrome.png" />
              <div class="txt">下载</div>
            </div>
          </CCButton>
          <CCButton style="margin-left: 20px" color="rgb(38,187,255)" class="download" @click="onClickEdge">
            <div class="list">
              <img src="./res/edge.png" />
              <div class="txt">下载</div>
            </div>
          </CCButton>
          <i @click="onClickGithub" class="iconfont icon_github github"></i>
        </div>
      </div>
      <iframe class="video" src="//player.bilibili.com/player.html?isOutside=true&aid=113803849106700&bvid=BV1jzcHeSEh3&cid=27797426092&p=1" scrolling="no" border="0" frameborder="no" framespacing="0" allowfullscreen="true"></iframe>
      <!-- <video class="video" controls="true" autoplay loop muted src="https://www.bilibili.com/video/BV1jzcHeSEh3/"></video> -->
    </div>
  </div>
</template>
<script lang="ts">
import ccui from "@xuyanfeng/cc-ui";
import { defineComponent, onMounted, ref } from "vue";
import PluginConfig from "../../cc-plugin.config";
const { CCInput, CCButton } = ccui.components;
export default defineComponent({
  name: "index",
  components: { CCButton },
  setup(props, { emit }) {
    onMounted(() => {
      updateLayout();
    });
    const horizontal = ref(true);
    function updateLayout() {
      const w = window.document.body.clientWidth;
      horizontal.value = w > 1100;
    }
    window.addEventListener("resize", updateLayout);
    const msg = ref(PluginConfig.manifest.name);
    const count = ref(0);
    const options = ref({
      background: {
        color: {
          value: "#000", // 粒子颜色
        },
      },
      fpsLimit: 60,
      interactivity: {
        events: {
          onClick: {
            enable: true,
            mode: "push", // 可用的click模式有: "push", "remove", "repulse", "bubble"。
          },
          onHover: {
            enable: true,
            mode: "grab", // 可用的hover模式有: "grab", "repulse", "bubble"。
          },
          resize: true,
        },
        modes: {
          bubble: {
            distance: 400,
            duration: 2,
            opacity: 0.8,
            size: 40,
          },
          push: {
            quantity: 4,
          },
          repulse: {
            distance: 200,
            duration: 0.4,
          },
        },
      },
      particles: {
        color: {
          value: "#ffffff",
        },
        links: {
          color: "#ffffff", // '#dedede'。线条颜色。
          distance: 150, // 线条长度
          enable: true, // 是否有线条
          opacity: 0.5, // 线条透明度。
          width: 1, // 线条宽度。
        },
        collisions: {
          enable: false,
        },
        move: {
          direction: "none",
          enable: true,
          outMode: "bounce",
          random: false,
          speed: 4, // 粒子运动速度。
          straight: false,
        },
        number: {
          density: {
            enable: true,
            area: 800,
          },
          value: 80, // 粒子数量。
        },
        opacity: {
          value: 0.5, // 粒子透明度。
        },
        shape: {
          type: "circle", // 可用的粒子外观类型有："circle","edge","triangle", "polygon","star"
        },
        size: {
          random: true,
          value: 5,
        },
      },
      detectRetina: true,
    });
    return {
      options,
      horizontal,
      msg,
      count,
      onClickChrome() {
        const url = "https://chromewebstore.google.com/detail/cc-inspector/hejbkamkfnkifppoaljcidepkhgaahcj?hl=zh-CN&utm_source=ext_sidebar";
        window.open(url);
      },
      onClickEdge() {
        const url = "https://microsoftedge.microsoft.com/addons/detail/ccinspector/jcghedjiinobccoffphdgkplcildapgb";
        window.open(url);
      },
      onClickGithub() {
        const url = "https://github.com/tidys/cc-inspector-chrome";
        window.open(url);
      },
    };
  },
});
</script>

<style scoped lang="less">
.panel {
  display: flex;
  flex-direction: column;
  overflow: auto;
  width: 100%;
  height: 100%;
  padding: 30px;
  box-sizing: border-box;
  background-color: black;
  .head {
    z-index: 1;
    display: flex;
    flex-direction: row;
    align-items: flex-end;
    .icon {
      width: 50px;
      height: 50px;
      padding-bottom: 8px;
    }
    .txt {
      color: #188ee1;
      font-size: 40px;
      font-weight: bold;
      margin-left: 10px;
    }
  }
  .content-row {
    flex-direction: row;
  }
  .content-col {
    flex-direction: column;
    .video {
      margin-top: 40px !important;
    }
  }
  .content {
    z-index: 1;
    display: flex;

    .title {
      margin-top: 10px;
      margin-left: 20px;
      min-width: 450px;
      box-sizing: border-box;
      .link {
        display: flex;
        flex-direction: row;
        align-items: flex-end;
        .github {
          cursor: pointer;
          padding: 0 20px;
          font-size: 30px;
          color: white;

          &:hover {
            color: #188ee1;
          }
          &:active {
            color: rgb(255, 153, 0);
          }
        }
        .download {
          width: 160px;
          height: 60px;
          font-size: 20px !important;
          display: flex;
          flex-direction: row;
          align-items: center;
          .list {
            display: flex;
            flex-direction: row;
            img {
              width: 50px;
              height: 50px;
            }
            .txt {
              display: flex;
              flex-direction: row;
              align-items: center;
              font-size: 20px;
              line-height: 22px;
              font-weight: normal;
              color: black;
            }
          }
        }
      }
    }
    .video {
      flex: 1;
      object-fit: cover;
      overflow: hidden;
      min-height: 440px;
      margin: 5px;
      box-sizing: border-box;
      color: white;
      border: 1px solid rgb(112, 112, 112);
      border-radius: 20px;
      box-shadow: 1px 1px 8px 2px;
    }
  }
}
</style>
