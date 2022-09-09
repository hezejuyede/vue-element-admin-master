<template>
  <div :class="leftStatus ? 'left-show':'left-hide'">
    <div class="left-show-div" @click="showLeft" v-if="leftStatus">
      <img src="../img/s-q.png" alt="" class="">
    </div>
    <div class="left-hide-div" @click="showLeft" v-if="!leftStatus">
      <img src="../img/zh-k.png" alt="" class="">
    </div>
    <div class="leftDiv">
      <div class="leftDivTop" ref="leftDivTop">
        <div class="leftDivTopTitle" ref="leftDivTopTitle">
          <div class="leftDivTopTitleL">行业选择</div>
          <div class="leftDivTopTitleC">
          </div>
          <div class="leftDivTopTitleR">
            <img src="../img/shou-q.png" alt="" v-if="showDown" @click="showBottom">
            <img src="../img/zhan-k.png" alt="" v-if="!showDown" @click="showBottom">
          </div>
        </div>
        <div class="leftDivTopBottom" v-if="showDown">
          <el-button style="width: 36px;height: 20px;padding: 0;font-size: 12px;float: left;margin-left: 2.5%; margin-top: 5px;" type="primary">查询</el-button>
          <div v-for="(item,index) in titleList" @click="chooseList(index,item.choose)"
               :class="(item.choose==='0') ? 'leftDivTopBottomDivChoose':'leftDivTopBottomDiv'">
            {{ item.name }}
          </div>
        </div>
      </div>
      <div class="leftDivBottom tree" ref="leftDivBottom">
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
          highlight-current
          node-key="id"
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
      leftStatus: this.leftState,
      showDown: true,
      chooseDiv: 0,
      titleList: [
        {'name': '全部', 'id': '0', 'choose': '0'},
        {"name": "钢铁", "id": "12", 'choose': '0'},
        {"name": "炼化", "id": "1", 'choose': '0'},
        {"name": "煤加工", "id": "3", 'choose': '0'},
        {"name": "焦化", "id": "2", 'choose': '0'},
        {"name": "煤电", "id": "16", 'choose': '0'},
        {"name": "肥料", "id": "5", 'choose': '0'},
        {"name": "轮胎", "id": "6", 'choose': '0'},
        {"name": "铁合金", "id": "13", 'choose': '0'},
        {"name": "水泥", "id": "7", 'choose': '0'},
        {"name": "石灰", "id": "8", 'choose': '0'},
        {"name": "玻璃", "id": "10", 'choose': '0'},
        {"name": "化学原料", "id": "4", 'choose': '0'},
        {"name": "陶瓷", "id": "11", 'choose': '0'},
        {"name": "有色", "id": "14", 'choose': '0'},
        {"name": "铸造", "id": "15", 'choose': '0'},
        {"name": "防水建材", "id": "9", 'choose': '0'},
      ],
      filterText: '',
      treeData: [
        {
          "id": 1,
          "label": "邹平地区企业",
          "children": [
            {
              "id": 101,
              "label": "邹平县晟昶钙业有限公司邹平县晟昶钙业有限公司邹平县晟昶钙业有限公司邹平县晟昶钙业有限公司"
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
      if (this.showDown) {
        this.$refs.leftDivBottom.style.height = '80%'
        this.$refs.leftDivTop.style.height = '20%'
      }else {
        this.$refs.leftDivTop.style.height = '50px'
        this.$refs.leftDivTopTitle.style.height = '50px'
        this.$refs.leftDivBottom.style.height = '90%'
      }
    },
    showLeft() {
      this.leftStatus = !this.leftStatus
      this.$emit('showLeft', this.leftStatus)
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
              let typeS = 1
              for (let j = 0; j < this.titleList.length; j++) {
                if (j > 0) {
                  if (this.titleList[j].choose === '0') {
                    typeS = 2
                  }
                  for (let n = 0; n < this.titleList.length; n++) {
                    if (n > 0) {
                      if (this.titleList[n].choose === '1') {
                        typeS = 1
                      }
                    }
                  }
                }
              }
              if (typeS === 2) {
                this.titleList[0].choose = '0'
              }
            }
          }
        }
      }
    },
    filterNode(value, data) {
      if (!value) return true
      return data.label.indexOf(value) !== -1
    },
    nodeClick(data, node, item) {
      if (data.children === undefined){}
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
<style lang="scss">
.el-tree-node__label {
  font-size: 12px;
  margin-top: 2px;
}

// 树形列表
.el-tree .el-tree-node__expand-icon.expanded {
  -webkit-transform: rotate(0deg);
  transform: rotate(0deg);
}

//有子节点 且未展开
.el-tree .el-icon-caret-right:before {
  background: url("./img/close.png") no-repeat 0 0;
  content: '';
  display: block;
  width: 16px;
  height: 16px;
  font-size: 16px;
  background-size: 16px;
  margin-left: 5px;
}

//有子节点 且已展开
.el-tree .el-tree-node__expand-icon.expanded.el-icon-caret-right:before {
  background: url("./img/open.png") no-repeat 0 0;
  content: '';
  display: block;
  width: 16px;
  height: 16px;
  font-size: 16px;
  background-size: 16px;
  margin-left: 5px;
}

//没有子节点
.el-tree .el-tree-node__expand-icon.is-leaf::before {
  background: transparent no-repeat 0 3px;
  content: '';
  display: block;
  width: 16px;
  height: 16px;
  font-size: 16px;
  background-size: 16px;
}

.tree {
  .el-tree-node {
    white-space: normal;

    .el-tree-node__content {
      height: 100%;
      padding-top: 5px;
      padding-bottom: 5px;
    }

    /* .el-tree-node__content:hover {
      background-color: #FFFFFF;
    }*/
    /* .el-tree-node:focus > .el-tree-node__content:hover {
      background-color: #FFFFFF;
    }*/
    /* .el-tree-node.is-current>.el-tree-node__content {
      background-color: #FFFFFF !important;
      color:#333!important
    }*/
    /*.el-tree--highlight-current .el-tree-node.is-current > .el-tree-node__content{
      background-color: #4a9de7 !important;
      color: #fff !important;
    }*/
    /* .el-tree--highlight-current .el-tree-node.is-current > .el-tree-node__content {
      background-color: red;
    }*/
  }
}
</style>
<style lang="scss" scoped>
.left-hide {
  width: 20%;
  position: relative;
  left: -18%;
  top: 0;
  height: 900px;
  transition: all 0.5s;
  z-index: 99;
}

.left-show {
  width: 20%;
  height: 900px;
  position: relative;
  left: 0;
  top: 0;
  transition: all 0.5s;
  z-index: 99;
  display: flex;
  align-items: flex-start;
  justify-content: center;


}

.left-show-div {
  width: 11%;
  height: 100%;
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
  z-index: 999;
}

.left-hide-div {
  width: 30px;
  height: 100%;
  background-color: #C6D6F5;
  position: absolute;
  top: 0;
  left: auto;
  bottom: 0;
  right: 0;
  margin: auto;
  display: flex;
  align-items: center;
  justify-content: flex-end;
  transition: all 0.5s;
}

.leftDiv {
  width: 85%;
  height: 100%;
  background-color: #FFFFFF;
  margin-left: 5%;
  .leftDivTop {
    height: 20%;
    .leftDivTopTitle {
      height: 30%;
      .leftDivTopTitleL {
        width: 43%;
        height: 100%;
        float: left;
        font-size: 16px;
        font-weight: bold;
        display: flex;
        align-items: center;
        justify-content: center;
      }
      .leftDivTopTitleC {
        width: 34%;
        height: 100%;
        float: left;
        font-size: 16px;
        font-weight: bold;
        display: flex;
        align-items: center;
        justify-content:center;
      }

      .leftDivTopTitleR {
        width: 23%;
        height: 100%;
        float: left;
        font-size: 16px;
        font-weight: bold;
        display: flex;
        align-items: center;
        justify-content: center;
        cursor: pointer;
      }
    }
    .leftDivTopBottom {
      height: 70%;
      padding-left: 4%;

      .leftDivTopBottomDiv {
        border: 1px solid #E6E6E6;
        float: left;
        height: 20px;
        margin-left: 2.5%;
        margin-top: 5px;
        padding-left: 2.2%;
        padding-right: 2.2%;
        font-size: 12px;
        display: flex;
        align-items: center;
        justify-content: center;
        cursor: pointer;
        border-radius: 2px;
      }

      .leftDivTopBottomDiv:nth-child(14),:nth-child(18) {
        padding-left: 8.5%;
        padding-right:8.5%;
      }


      .leftDivTopBottomDivChoose {
        color: #588CFD;
        border: 1px solid #588CFD;
        float: left;
        height: 20px;
        margin-left: 2.5%;
        margin-top: 5px;
        padding-left: 2.25%;
        padding-right: 2.25%;
        font-size: 12px;
        display: flex;
        align-items: center;
        justify-content: center;
        cursor: pointer;
        border-radius: 2px;
      }

      .leftDivTopBottomDivChoose:nth-child(14),:nth-child(18) {
        padding-left: 8.5%;
        padding-right:8.5%;
      }

    }
  }

  .leftDivBottom {
    height: 80%;
    width: 100%;
    padding-top: 10px;
    border-top: 3px solid #ECECEC;
    overflow: auto;
  }

}

</style>
