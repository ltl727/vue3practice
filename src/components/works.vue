<template>
  <div id="works">
  <h1 style="font-size: 24px; margin-bottom: 20px;">任务管理系统</h1>
  <div id="search" style="margin: auto;width: auto;">
<el-input v-model="newtitle"  style="width: auto;"></el-input><el-button round type="primary" @click="doSearch">搜索</el-button>
</div>
<el-table :data="search" stripe border highlight-current-row style="width: 100%; border-radius: 12px; box-shadow: 0 4px 12px rgba(0,0,0,0.05);">
<el-table-column prop="id" label="ID" min-width="150" align="center" show-overflow-tooltip></el-table-column>
<el-table-column prop="title" label="任务名称" min-width="200" align="center" show-overflow-tooltip></el-table-column>
<el-table-column prop="content" label="任务内容" min-width="300" align="center" show-overflow-tooltip></el-table-column>
<el-table-column prop="category" label="分类" min-width="150" align="center" show-overflow-tooltip></el-table-column>
<el-table-column align="center">   
<template #default="scope">
          <el-button round 
            size="small" 
            type="danger" 
            @click="deleteid(scope.row.id)"
          >
            删除
          </el-button>
        </template></el-table-column>

<el-table-column>   
<template #default="scope">
          <el-button round 
            size="small" 
            @click="edit(scope.row.id)"
          >
            编辑
          </el-button>
        </template></el-table-column>
</el-table>
<div style="margin: auto;width: auto;" id="add">
<h2 id="addwork">添加任务</h2>
<el-input v-model="titleData" placeholder="任务名称" style="width: auto;">
</el-input>
<el-input v-model="contentData" placeholder="任务内容"  style="width: auto;">
</el-input>
<el-radio-group v-model="radio">
<el-radio label="学习">学习</el-radio>
<el-radio label="生活">生活</el-radio>
<el-radio label="艺术">艺术</el-radio>
</el-radio-group>
<el-button round type="primary" @click="add">添加任务</el-button>
<el-button round v-if="isedit" type="primary" @click="submit">提交编辑后的任务</el-button>
<el-button round type="primary" @click="reset">重置</el-button>
</div>
  </div>
</template>

<script>
import { ref } from 'vue'
import { computed } from 'vue'
export default {
  name: 'HelloWorld',
  setup(){
 const radio=ref('')
 const titleData=ref('')
 const contentData=ref('')
 const keyword=ref('')
 const newtitle=ref('')
 const titlebefore=ref('')
 const editid=ref(false)
 const isedit=ref(false)
 const works = ref([
  {
    "id": 1,
    "title": "学习Vue3组合式API",
    "content": "掌握Vue3的组合式API使用，包括setup、ref、reactive等核心概念",
    "category": "学习"
  },
  {
    "id": 2,
    "title": "完成项目架构设计",
    "content": "设计项目的整体架构和组件结构",
    "category": "学习"
  },
  {
    "id": 3,
    "title": "周末大扫除",
    "content": "整理房间，清洗衣物，打扫厨房和卫生间",
    "category": "生活"
  },
  {
    "id": 4,
    "title": "学习Pinia状态管理",
    "content": "掌握Pinia的核心概念，包括store的定义、state、getters、actions的使用",
    "category": "学习"
  },
  {
    "id": 5,
    "title": "参观美术馆展览",
    "content": "参观现代艺术展览，欣赏油画和雕塑作品",
    "category": "艺术"
  },
  {
    "id": 6,
    "title": "超市购物",
    "content": "购买下周的食材和生活用品，包括蔬菜、水果、牛奶等",
    "category": "生活"
  },
  {
    "id": 7,
    "title": "学习Vue Router",
    "content": "掌握Vue Router的基础使用，包括路由配置、导航守卫和动态路由",
    "category": "学习"
  },
  {
    "id": 8,
    "title": "练习水彩画",
    "content": "完成一幅水彩风景画练习，重点练习色彩渐变和层次感",
    "category": "艺术"
  },
  {
    "id": 9,
    "title": "缴纳水电费",
    "content": "通过网上银行缴纳本月的水电费和燃气费",
    "category": "生活"
  },
  {
    "id": 10,
    "title": "阅读设计原理书籍",
    "content": "阅读《设计心理学》前两章，并做读书笔记",
    "category": "艺术"
  }
])
const initdata = () =>{
 if(localStorage.getItem('works')){
  works.value=JSON.parse(localStorage.getItem('works'))
 }else{
  localStorage.setItem('works',JSON.stringify(works.value))
 }
}

initdata()
const ifexist = (data) =>{
  const data1=works.value.find(task => task.title === data.title)
  if(data1){
    return true
  }
  else{
    return false
  }
}
const exist = () =>{
  if(titleData.value&&contentData.value&&radio.value){
    return true
  }
  else{
    return false
  }
}
const reset = () =>{
  titleData.value=''
  contentData.value=''
  radio.value=''
  isedit.value=false
}
const add = () =>{
  if(ifexist({title:titleData.value,content:contentData.value,category:radio.value})){
    alert('任务名称已存在')
    return
  }
  if(!exist()){
    alert('请填写完整信息')
    return
  }
  if(works.value.length==0){
    works.value.push({
      id:1,
      title:titleData.value,
      content:contentData.value,
      category:radio.value
    })
      localStorage.setItem('works',JSON.stringify(works.value))
  }
  else{
  works.value.push({
    id:works.value[works.value.length-1].id+1,
    title:titleData.value,
    content:contentData.value,
    category:radio.value
  })
  localStorage.setItem('works',JSON.stringify(works.value))
  titleData.value=''
contentData.value=''
radio.value=''
}}
const deleteid = (id) =>{
  const index = works.value.findIndex(task => task.id === id)
  if(index !== -1){
    works.value.splice(index,1)
    localStorage.setItem('works', JSON.stringify(works.value))
  }
}

const edit = (id) =>{
  isedit.value=true
  const data=works.value.find(task => task.id === id)
  titleData.value=data.title
  contentData.value=data.content
  radio.value=data.category
  editid.value=data.id

  titlebefore.value=data.title



  }
  const submit= () =>{
    if(!isedit.value){
      alert('请先编辑任务')
      return
    }
     if(!exist()){
      alert('请填写完整信息')
      return
    }
    if(ifexist({title:titleData.value,content:contentData.value,category:radio.value})){
      if(!(titlebefore.value==titleData.value)){
        alert('任务名称已存在')
        return
      }
    }
     const data=works.value.find(task => task.id === editid.value)
     const id=data.id
     works.value.forEach(work => {
      if(id==work.id){
        work.title=titleData.value
        work.content=contentData.value
        work.category=radio.value
      }
     })
       localStorage.setItem('works', JSON.stringify(works.value))
     titleData.value=''
     contentData.value=''
     radio.value=''
  editid.value = null
titlebefore.value = ''
isedit.value=false
  }

    const search = computed(() => {
      if (!keyword.value) return works.value
      const kw = keyword.value.toLowerCase()
     
      return works.value.filter(work => 
        work.title.toLowerCase().includes(kw) || 
        work.content.toLowerCase().includes(kw)
      )
    })


    const doSearch = () => {
      keyword.value = newtitle.value
    }

  return{
    works,
    radio,
    titleData,
    contentData,
    add,
    deleteid,
    edit,
    submit,
    search,
    keyword,
    newtitle,
    doSearch,
    titlebefore,
    ifexist,
    exist,
    initdata,
    editid,
    reset,
    isedit
  }
}
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
#works{
  display: flex;
  flex-direction: column;
  border-radius: 12px;
  max-width: 1200px;
  margin: 0 auto;
  padding: 20px;
  background-color: white;
  min-height: 100vh;
}
#addwork{
font-size: 20px;
}
#search{
  flex-direction: row;
  padding: 10px;
}
#add{
  flex-direction: row;
}
body {
  font-family: 'Inter', -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Helvetica, Arial, sans-serif;
}
</style>