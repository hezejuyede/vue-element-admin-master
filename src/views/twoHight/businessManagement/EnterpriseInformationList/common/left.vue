<template>
  <div :class="leftState ? 'left-show':'left-hide'">
    <div class="left-show-div" @click="showLeft" v-if="leftState">
      <img src="../img/s-q.png" alt="" class="">
    </div>
    <div class="left-hide-div" @click="showLeft" v-if="!leftState">
      <img src="../img/zh-k.png" alt="" class="">
    </div>
    <div class="leftDiv">
      <div class="leftDivTop">
        <div class="leftDivTopTitle">
          <div class="leftDivTopTitleL">行业选择</div>
          <div class="leftDivTopTitleR">
            <img src="../img/shou-q.png" alt="" v-if="showDown" @click="showBottom">
            <img src="../img/zhan-k.png" alt="" v-if="!showDown" @click="showBottom">
          </div>
        </div>
        <div class="leftDivTopBottom" v-if="showDown">
          <div v-for="(item,index) in titleList" @click="chooseList(index,item.choose)"
               :class="(item.choose==='0') ? 'leftDivTopBottomDivChoose':'leftDivTopBottomDiv'">
            {{ item.name }}
          </div>
        </div>
      </div>
      <div class="leftDivBottom">
        <el-input
          style="width: 90%;margin: 10px 5% 10px 5%"
          placeholder="输入关键字进行过滤"
          v-model="filterText">
          <i slot="prefix" class="el-input__icon el-icon-search"></i>
        </el-input>
        <el-tree
          class="filter-tree"
          :data="treeData"
          :props="defaultProps"
          accordion
          @node-click="nodeClick"
          :filter-node-method="filterNode"
          ref="tree">
        </el-tree>
      </div>
    </div>
  </div>

</template>

<script type="text/ecmascript-6">
export default {
  name: 'Modal',
  data() {
    return {
      showDown: true,
      chooseDiv: 0,
      titleList: [
        {'name': '全部', 'id': '0', 'choose': '0'},
        {"name": "钢铁", "id": "12", 'choose': '1'},
        {"name": "炼化", "id": "1", 'choose': '1'},
        {"name": "焦化", "id": "2", 'choose': '1'},
        {"name": "煤电", "id": "16", 'choose': '1'},
        {"name": "肥料", "id": "5", 'choose': '1'},
        {"name": "轮胎", "id": "6", 'choose': '1'},
        {"name": "水泥", "id": "7", 'choose': '1'},
        {"name": "石灰", "id": "8", 'choose': '1'},
        {"name": "玻璃", "id": "10", 'choose': '1'},
        {"name": "陶瓷", "id": "11", 'choose': '1'},
        {"name": "有色", "id": "14", 'choose': '1'},
        {"name": "铸造", "id": "15", 'choose': '1'},
        {"name": "煤加工", "id": "3", 'choose': '1'},
        {"name": "铁合金", "id": "13", 'choose': '1'},
        {"name": "化学原料", "id": "4", 'choose': '1'},
        {"name": "防水建材", "id": "9", 'choose': '1'},
      ],
      filterText: '',
      treeData: [
        {
          "id": 1,
          "label": "邹平地区企业",
          "children": [
            {
              "id": 101,
              "label": "邹平县晟昶钙业有限公司"
            },
            {
              "id": 102,
              "label": "邹平县顺通建筑陶瓷有限公司"
            },
            {
              "id": 103,
              "label": "邹平县顺鑫建筑陶瓷有限公司"
            },
            {
              "id": 104,
              "label": "邹平县台子福利醋酸加工厂"
            },
            {
              "id": 105,
              "label": "邹平县永顺建筑陶瓷厂"
            },
            {
              "id": 106,
              "label": "邹平兴发氧化钙有限公司"
            },
            {
              "id": 107,
              "label": "邹平伊文华源金属科技有限公司"
            },
            {
              "id": 108,
              "label": "邹平元亨钙业有限公司"
            },
            {
              "id": 109,
              "label": "邹平长山实业有限公司"
            },
            {
              "id": 110,
              "label": "邹平中科纳米材料有限公司"
            }
          ]
        },
        {
          "id": 2,
          "label": "沾化地区企业",
          "children": [
            {
              "id": 201,
              "label": "华能沾化热电有限公司"
            },
            {
              "id": 202,
              "label": "山东昌达化工有限公司"
            },
            {
              "id": 203,
              "label": "山东海明化工有限公司"
            },
            {
              "id": 204,
              "label": "山东陆源化工有限公司"
            },
            {
              "id": 205,
              "label": "山东通远化工有限公司"
            },
            {
              "id": 206,
              "label": "山东炜烨热电有限公司"
            },
            {
              "id": 207,
              "label": "山东沾化奥仕化学有限公司"
            },
            {
              "id": 208,
              "label": "山东沾化崇正水泥有限公司"
            },
            {
              "id": 209,
              "label": "山东沾化泰和化工有限公司"
            },
            {
              "id": 210,
              "label": "山东沾化腾越石油化工有限责任公司"
            }
          ]
        },
        {
          "id": 3,
          "label": "信阳地区企业",
          "children": [
            {
              "id": 301,
              "label": "阳信隆丰金属制品有限公司"
            },
            {
              "id": 302,
              "label": "滨州科乘化工有限公司"
            },
            {
              "id": 304,
              "label": "滨州市阳信县华兴石油有限公司"
            },
            {
              "id": 304,
              "label": "阳信东泰精密金属有限公司"
            },
            {
              "id": 305,
              "label": "山东巨久能源科技有限公司"
            },
            {
              "id": 306,
              "label": "山东科宇能源有限公司"
            },
            {
              "id": 307,
              "label": "山东省阳信恒源石油制品有限公司"
            },
            {
              "id": 308,
              "label": "山东魏桥铝电有限公司"
            },
            {
              "id": 309,
              "label": "泰安鲁珠水泥有限公司阳信分公司"
            },
            {
              "id": 310,
              "label": "阳信昌泽化工有限公司"
            }
          ]
        },
        {
          "id": 4,
          "label": "无棣地区企业",
          "children": [
            {
              "id": 401,
              "label": "无棣县欣旺达金属制品有限公司"
            },
            {
              "id": 402,
              "label": "大唐鲁北发电有限责任公司"
            },
            {
              "id": 403,
              "label": "山东鲁北海生生物有限公司"
            },
            {
              "id": 404,
              "label": "山东鲁北企业集团总公司"
            },
            {
              "id": 405,
              "label": "山东三岳化工有限公司"
            },
            {
              "id": 406,
              "label": "山东无棣齐星高科技铝材有限公司"
            },
            {
              "id": 407,
              "label": "无棣县新星热电有限责任公司"
            },
            {
              "id": 408,
              "label": "无棣鑫岳化工有限公司"
            },
            {
              "id": 409,
              "label": "无棣鑫岳燃化有限公司"
            },
            {
              "id": 410,
              "label": "无棣众诚供热有限公司"
            }
          ]
        },
        {
          "id": 5,
          "label": "惠民地区企业",
          "children": [
            {
              "id": 501,
              "label": "惠民县广嘉金属磨料有限公司"
            },
            {
              "id": 502,
              "label": "惠民县汇宏新材料有限公司"
            },
            {
              "id": 503,
              "label": "惠民县金滟新材料有限公司"
            },
            {
              "id": 504,
              "label": "惠民县熠彩机械有限公司"
            },
            {
              "id": 505,
              "label": "惠民县展成钙业有限公司"
            },
            {
              "id": 506,
              "label": "惠民县忠泉建材有限公司"
            },
            {
              "id": 507,
              "label": "山东钰鑫金属磨料科技有限公司"
            },
            {
              "id": 508,
              "label": "惠民县开元精密铸造有限公司"
            },
            {
              "id": 509,
              "label": "山东乾晟金属制品有限公司"
            },
            {
              "id": 510,
              "label": "滨州市永杰钙业有限公司"
            }
          ]
        },
        {
          "id": 6,
          "label": "博兴地区企业",
          "children": [
            {
              "id": 601,
              "label": "京博控股集团有限公司"
            },
            {
              "id": 602,
              "label": "山东博兴胜利科技有限公司"
            },
            {
              "id": 603,
              "label": "山东成达新能源科技有限公司"
            },
            {
              "id": 604,
              "label": "山东国盛陶瓷科技发展有限公司"
            },
            {
              "id": 605,
              "label": "山东京博石油化工有限公司"
            },
            {
              "id": 606,
              "label": "山东聚博建陶有限公司"
            },
            {
              "id": 607,
              "label": "山东联众陶瓷有限公司"
            },
            {
              "id": 608,
              "label": "山东盛和热能有限公司"
            },
            {
              "id": 609,
              "label": "山东泰山新型建材有限公司"
            },
            {
              "id": 610,
              "label": "山东香驰热动有限公司"
            }
          ]
        },
        {
          "id": 7,
          "label": "滨城地区企业",
          "children": [
            {
              "id": 701,
              "label": "滨化集团股份有限公司"
            },
            {
              "id": 702,
              "label": "滨州滨北热电有限公司"
            },
            {
              "id": 703,
              "label": "滨州金安热电有限公司"
            },
            {
              "id": 704,
              "label": "滨州山水水泥有限公司"
            },
            {
              "id": 705,
              "label": "滨州市鑫力活塞有限公司"
            },
            {
              "id": 706,
              "label": "大唐滨州发电有限公司"
            },
            {
              "id": 707,
              "label": "滨州市五环镶圈制造有限公司"
            },
            {
              "id": 708,
              "label": "滨州滨渤耐磨合金有限公司"
            },
            {
              "id": 709,
              "label": "滨州东海龙活塞有限公司"
            },
            {
              "id": 710,
              "label": "滨州市东城精密铸造有限公司"
            }
          ]
        }
      ],
      defaultProps: {
        children: 'children',
        label: 'label'
      }
    }
  },
  mounted() {
    this.getList()
  },
  created() {

  },
  watch: {
    filterText(val) {
      this.$refs.tree.filter(val)
    }
  },
  methods: {
    getList() {
    },
    showBottom() {
      this.showDown = !this.showDown
    },
    showLeft() {
      this.leftState = !this.leftState
      this.$emit('showLeft', this.leftState)
    },
    chooseList(index, choose) {
      if (index === 0) {
        for (let i = 0; i < this.titleList.length; i++) {
          if (this.titleList[i].choose !== '0') {
            for (let j = 0; j < this.titleList.length; j++) {
              this.titleList[j].choose = '0'
            }
          } else {
            for (let j = 0; j < this.titleList.length; j++) {
              this.titleList[j].choose = '1'
            }
          }
        }
      } else {
        for (let i = 0; i < this.titleList.length; i++) {
          if (index === i) {
            if (choose === '0') {
              this.titleList[i].choose = '1'
              this.titleList[0].choose = '1'
            } else {
              this.titleList[i].choose = '0'
              if (this.titleList[0].choose === '1') {
                for (let j = 0; j < this.titleList.length; j++) {
                  if (this.titleList[j].choose === '1' && j > 0) {
                    return
                  } else if (this.titleList[j].choose === '1' && j === 0) {
                    return
                  } else {
                    this.titleList[0].choose = '0'
                  }
                }
              }
            }
          }
        }
      }
    },
    filterNode(value, data) {
      if (!value) return true
      return data.label.indexOf(value) !== -1;
    },
    nodeClick(data, node, item) {
      if (data.children === undefined) {
      }
    }
  },
  // eslint-disable-next-line no-undef
  props: {
    leftState: {
      type: Boolean,
      required: true
    }
  }
}
</script>
<style lang="scss" scoped>
.left-hide{
  width: 20%;
  position: relative;
  left: -18%;
  top: 0;
  height: 800px;
  transition: all 0.5s;
  z-index: 99;
}
.left-show{
  width: 20%;
  height: 800px;
  position: relative;
  left: 0;
  top: 0;
  transition: all 0.5s;
  z-index: 99;
  display: flex;
  align-items: flex-start;
  justify-content: center;

}
.left-show-div{
  width: 30px;
  height:100%;
  position: absolute;
  top: 0;
  left: 0;
  bottom: 0;
  right: auto;
  margin: auto;
  display: flex;
  align-items: center;
  justify-content: flex-start;
  transition: all 0.5s;
  background-color: #C6D6F5;
}
.left-hide-div{
  width: 30px;
  height:100%;
  background-color: #C6D6F5;
  position: absolute;
  top: 0;
  left: auto;
  bottom: 0;
  right: 0;
  margin: auto;
  display: flex;
  align-items: center;
  justify-content:flex-end;
  transition: all 0.5s;
}
.leftDiv {
  width: 80%;
  height: 98%;
  background-color: #FFFFFF;
  .leftDivTop{
    .leftDivTopTitle {
      height: 50px;
      .leftDivTopTitleL {
        width: 50%;
        height: 100%;
        float: left;
        font-size: 16px;
        font-weight: bold;
        display: flex;
        align-items: center;
        justify-content: flex-start;
        padding-left: 10px;
      }

      .leftDivTopTitleR {
        width: 50%;
        height: 100%;
        float: left;
        font-size: 16px;
        font-weight: bold;
        display: flex;
        align-items: center;
        justify-content: flex-end;
        padding-right: 10px;
        cursor: pointer;
      }
    }
    .leftDivTopBottom {
      height: 250px;
      .leftDivTopBottomDiv {
        float: left;
        width: 30%;
        height: 30px;
        padding: 5px 10px;
        margin: 4px;
        background-color: #F7F7F7;
        font-size: 12px;
        display: flex;
        align-items: center;
        justify-content: center;
        cursor: pointer;
        border-radius: 2px;
      }
      .leftDivTopBottomDiv:nth-child(16), :nth-child(17) {
        width: 45%;
      }

      .leftDivTopBottomDivChoose {
        color: #FFFFFF;
        float: left;
        width: 30%;
        height: 30px;
        padding: 5px 10px;
        margin: 4px;
        background-color: #3377FF;
        font-size: 12px;
        display: flex;
        align-items: center;
        justify-content: center;
        cursor: pointer;
        border-radius: 2px;
      }

      .leftDivTopBottomDivChoose:nth-child(16), :nth-child(17) {
        width: 45%;
      }
    }
  }
  .leftDivBottom {
    height: 60%;
    width: 100%;
    padding-top: 20px;
    border-top: 3px solid #ECECEC;
    overflow: auto;
  }

}

</style>
