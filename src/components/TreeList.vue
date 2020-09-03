<template>
  <div class="treebox">
    <ul>
      <li v-for="(item,index) in folder" :key="index">
        <i v-if="item.children" :class="item.show ? 'active':''">
          <svg viewBox="0 0 1024 1024" version="1.1" xmlns="http://www.w3.org/2000/svg" width="20" height="20">
            <path d="M597.333333 529.749333c18.176-15.146667 18.432-39.552 0-54.912L407.168 316.416c-18.218667-15.146667-32.981333-8.021333-32.981333 15.018667v341.76c0 23.424 14.506667 30.336 32.981333 14.976l190.08-158.421334z"></path>
          </svg>
        </i>
        <p @click="select(item)">
          <span>{{ item.label }}</span>
        </p>
        <treelist v-if="item.show" :folder="item.children" :select="select"></treelist>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  props: ['folder', 'select'],
  name: 'treelist',
  methods: {
    // js动态生成
    arr2div (arrs, fname) {
      const div = document.createElement('div')
      div.classList.add(fname)
      // 递归函数
      function children2div (arrs, divs) {
        for (let i = 0; i < arrs.length; i++) {
          const div = document.createElement('div')
          div.classList.add(`${arrs[i].name}`)
          div.innerText = arrs[i].text
          if (arrs[i].children && arrs[i].children.length > 0) {
            const newarrs = arrs[i].children
            children2div(newarrs, div)
          }
          divs.appendChild(div)
        }
      }
      children2div(arrs, div)
      return div
    }
  }
}
</script>

<style scoped>
.treebox ul {
  list-style: none;
  margin: 0;
  padding: 0 20px;
}
.treebox ul li {
  cursor: pointer;
  padding: 5px 0;
  margin: 5px 0;
  position: relative;
}
.treebox ul li p {
  margin: 0;
  position: relative;
}
.treebox ul li i {
  position: absolute;
  top: 5px;
  left: -20px;
}
.treebox .active {
  transform: rotate(90deg);
  transform-origin: center;
  transition: transform 0.3s;
}
</style>
