<template>
  <div>
    <div>
      <div
        class="fjsb"
        style="padding:3vw;background: #f5f5f5;border: solid #E4E4E4;border-width: 1px 0"
        @click="filter = !filter"
      >
        <span class="grayFont">{{ location }}</span>
        <div class="arrow down" :class="[filter ? 'up' : 'down']"></div>
      </div>
      <transition-group name="slide-fade">
        <div v-for="(item, index) in school" :key="index" v-show="!filter" class="bbe">
          <router-link
            v-if="item.jz_num"
            class="dib fac school-container"
            :to="{
              path: 'jianzhanglist',
              query: { schoolid: item.id, schoolname: item.title }
            }"
          >
            <img
              v-lazy="item.thumb"
              :key="item.thumb"
              class="school-logo"
              alt=""
            />
            <div class="tl">
              <p class="fac t">
                <span class="f16 fc666">{{ item.title }}</span>
                <span
                  class="brand brand-211 whiteFont"
                  v-if="item.school_attribute.includes('211')"
                  >211</span
                >
                <span
                  class="brand brand-985 whiteFont"
                  v-if="item.school_attribute.includes('985')"
                  >985</span
                >
              </p>
              <p class="grayFont">{{ item.jz_num }}篇简章</p>
            </div>
          </router-link>
          <router-link
            v-else
            class="dib fac school-container"
            :to="{
              path: 'kuaisujz',
              query: { id: item.id, schoolname: item.title, type: type }
            }"
          >
            <img
              v-lazy="item.thumb"
              :key="item.thumb"
              class="school-logo"
              alt=""
            />
            <div class="tl">
              <p class="fac t">
                <span class="f16 fc666">{{ item.title }}</span>
              </p>
            </div>
          </router-link>
        </div>
      </transition-group>
    </div>
  </div>
</template>

<script>
export default {
  name: "SchoolListBlock",
  props: {
    location: String,
    school: null,
    type: null
  },
  data() {
    return {
      filter: false
    };
  },
  methods: {}
};
</script>

<style scoped lang="scss">
.arrow {
  width: 3vw;
  height: 3vw;
  border-right: 1px solid #b0b0b0;
  border-bottom: 1px solid #b0b0b0;
  transition: all 0.3s;
}
.arrow.down {
  transform: rotate(45deg);
}
.arrow.up {
  transform: rotate(-135deg);
  /*transform: rotate(225deg);*/
}
.school-container {
  padding: 3vw;
  .t {
    margin-bottom: 1vw;
  }
}
.bbe + .bbe {
  border-top: 1px solid #e4e4e4;
}
.school-logo {
  width: 9.6vw;
  height: 9.6vw;
  object-fit: contain;
  margin-right: 3vw;
}
.brand {
  display: inline-block;
  width: 7.2vw;
  line-height: 3.6vw;
  border-radius: 3px;
  text-align: center;
  margin-left: 2vw;
}
.brand-211 {
  background: #4f99dc;
}
.brand-985 {
  background: #e65757;
}
</style>
