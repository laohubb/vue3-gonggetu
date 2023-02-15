<script setup>
import { ref, computed, onMounted } from 'vue';

const rows = ref(4); // 横向数
const columns = ref(3); // 竖向数
const imgWidth = ref(''); // 分割小块初始宽高
const imgHeight = ref(''); // 分割小块初始宽高
const album = ref([]); // 存放小块位置的数组
const Iboxwidth = ref(''); // 暂存原图宽
const Iboxheight = ref(''); // 暂存原图高
const gap = ref(10)   //间距

const imageUrl = '../src/assets/images/p1.png'
//计算带有边框的容器宽
const boxwidth = computed(() => {
  return Iboxwidth.value + rows.value * gap.value;
});

//计算带有边框的容器高
const boxheight = computed(() => {
  return Iboxheight.value + columns.value * gap.value;
});

const photograph = () => {
  // 借助Image对象
  const img_url = imageUrl
  const img = new Image();
  img.src = img_url;
  // 通过计时器获取原图的宽高
  const setImg = setInterval(() => {
    if (img.width > 0) {
      // 拿到原图信息关闭计时器
      clearInterval(setImg);
      // 暂存一下图片宽高
      Iboxwidth.value = img.width;
      Iboxheight.value = img.height;
      //计算
      imgWidth.value = img.width / rows.value; // 计算出小块宽
      imgHeight.value = img.height / columns.value; // 计算出小块高
      handle();
    }
  }, 100);
};

const handle = () => {
  // 竖向小块个数在外层
  for (let h = 0; h < columns.value; h++) {
    // 横向小块个数
    for (let w = 0; w < rows.value; w++) {
      // 组成带有坐标的'块'数组用于页面展示
      album.value.push({
        Iwidth: -w * imgWidth.value + "px",
        Iheight: -h * imgHeight.value + "px",
      });
    }
  }
};

onMounted(() => {
  photograph();
});

</script>


<template>

  <transition-group tag="div" name="el-zoom-in-center" duration="2000" class="grid" :style="{
    width: boxwidth + 'px',
    height: boxheight + 'px',
    marginLeft: '10px',
    overflow: 'hidden',
  }">
    <div class="flypicture" :style="{
      background: 'url(' + imageUrl + ') ' + item.Iwidth + ' ' + item.Iheight,
      height: `${imgHeight}px}`,
      width: `${imgWidth}px`,
      marginRight: `${gap}px`,
      marginTop: `${gap}px`,
    }" v-for="(item, index) in album" :key="index"></div>
  </transition-group>

</template>

<style scoped>


.grid {
  display: flex;
  flex-wrap: wrap;
  margin-bottom: 30px;
}
</style>
