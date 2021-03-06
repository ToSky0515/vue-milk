<style lang="less">
.demo-menu{
  .vm-menu{
  }
  .menu-active{
    .vm-nav-bar,
    .vm-menu{
      position:relative;
      z-index:100 !important;
    }
    .menu-mask{
      display:block;
      z-index:99;
    }
  }
  .menu-mask{
      display:none;
      position: fixed;
      top: 0;
      width: 100%;
      height: 100%;
      background-color: #000;
      opacity: 0.4;
  }
}
</style>
<script>
import { Toast } from 'packages';
export default {
  data(){
    return {
      itemList:[
        {
          label:'menu1',
          value:'m1',
          children:[
            {
              label:'child1',
              value:'c1'
            },
            {
              label:'child2',
              value:'c2'
            },
            {
              label:'child3',
              value:'c3'
            },
            {
              label:'child4',
              value:'c4'
            },
            {
              label:'child5',
              value:'c5'
            },
            {
              label:'child6',
              value:'c6'
            },
            {
              label:'child7',
              value:'c7'
            },
            {
              label:'child8',
              value:'c8'
            },
            {
              label:'child9',
              value:'c9'
            }
          ]
        },
        {
          label:'menu2',
          value:'m2',
          children:[
            {
              label:'child21',
              value:'c21'
            },
            {
              label:'child22',
              value:'c22',
              disabled:true
            },
            {
              label:'child23',
              value:'c23'
            }
          ]
        },
        {
          label:'menu3',
          value:'m3'
        }
      ],
      selectItem:[1],
      oneShow:false,
      twoShow:false,
      threeShow:false
    }
  },
  methods:{
    toastInfo:function(info){
      console.log(info);
    },
    changeMenu:function(menu){
      this[menu]=!this[menu];
    }
  }
}
</script>
## Toast ??????

### ????????????

```javascript
import { Menu } from 'milk-vue';
Vue.component(Menu.name, Menu);
```

### ????????????

```javascript
import { Toast } from 'packages';
export default {
  data(){
    return {
      itemList:[
        {
          label:'menu1',
          value:'m1',
          children:[
            {
              label:'child1',
              value:'c1'
            },
            {
              label:'child2',
              value:'c2'
            },
            {
              label:'child3',
              value:'c3'
            },
            {
              label:'child1',
              value:'c4'
            },
            {
              label:'child2',
              value:'c5'
            },
            {
              label:'child3',
              value:'c6'
            },
            {
              label:'child1',
              value:'c7'
            },
            {
              label:'child2',
              value:'c8'
            },
            {
              label:'child3',
              value:'c9'
            }
          ]
        },
        {
          label:'menu2',
          value:'m2'
        }
      ],
      selectItem:[1],
      oneShow:false
    }
  },
  methods:{
    toastInfo:function(info){
      console.log(info);
    },
    changeMenu:function(menu){
      this[menu]=!this[menu];
    }
  }
}
```

### ????????????

???????????????`menu-data`?????????????????????`change`?????????????????????

:::demo ??????

```html
<div :class="oneShow?'menu-active':''">
    <div class="menu-mask"></div>
    <v-nav-bar
      :icon="oneShow?'left':'right'"
      title="Normal menu"
      @icon-click="changeMenu('oneShow')"
    >
    </v-nav-bar>
    <v-menu
      v-show="oneShow"
      :menu-data="itemList"
      @change="toastInfo"
    >
    </v-menu>
<div>
```
:::

### ????????????

`level`??????????????????

:::demo ????????????

```html
<div :class="twoShow?'menu-active':''">
    <div class="menu-mask"></div>
    <v-nav-bar
      :icon="twoShow?'left':'right'"
      title="Single menu"
      @icon-click="changeMenu('twoShow')"
    >
    </v-nav-bar>
    <v-menu
      v-show="twoShow"
      :menu-data="itemList"
      :level="1"
      @change="toastInfo"
    >
    </v-menu>
<div>
```
:::

### ????????????

`multi-select`?????????????????????

:::demo ????????????

```html
<div :class="threeShow?'menu-active':''">
    <div class="menu-mask"></div>
    <v-nav-bar
      :icon="threeShow?'left':'right'"
      title="Multi-select menu"
      @icon-click="changeMenu('threeShow')"
    >
    </v-nav-bar>
    <v-menu
      v-show="threeShow"
      :menu-data="itemList"
      multi-select
      @change="toastInfo"
      @ensure="toastInfo"
      @cancel="changeMenu('threeShow')"
    >
    </v-menu>
<div>
```
:::

### API

| ?????? | ?????? | ?????? | ????????? | ????????? |
|-----------|-----------|-----------|-------------|-------------|
| menu-data | ???????????? | `Array<{label: String, value, disabled?, children<data>?}>` | [] | - |
| multi-select | ?????????????????? | `Boolean` | `false` | `false`,`true` |
| level | ???????????? | `Number` | `2` | `1`,`2` |
| height | ???????????? | `Number` | `document.documentElement.clientHeight / 2` | - |

### Event

| ???????????? | ?????? | ???????????? |
|-----------|-----------|-----------|
| change | ???????????????????????????????????? | ??????????????????1?????????:String???1?????????:Array???2???:Object<1?????????value: 2?????????value>??? |
| ensure | ????????????????????????`??????`??????????????? | ??????????????????1?????????:String???1?????????:Array???2???:Object<1?????????value: 2?????????value>??? |
| cancel | ????????????????????????`??????`??????????????? | - |
