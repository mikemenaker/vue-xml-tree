<template>
  <div class="xml-tree">
    <div v-if="children.length > 0" class="root_elem">
      <div v-if="elem.nodeType === 1 && isText">
        <span class="xml-tree-tag">&lt;{{ elem.nodeName }}</span>
        <span v-if="elem.hasAttributes()">
            <span v-for="(attribute, index) in elem.attributes" :key="index">
             <span class="xml-tree-attr">&nbsp;{{attribute.name}}</span>
             <span>=</span>
             <span class="xml-tree-attr">"{{attribute.value}}"</span>
             </span>
        </span>
        <span class="xml-tree-tag">></span>
        <span>{{ this.children[0].data.trim() }}</span>
        <span class="xml-tree-tag">&lt;/{{ elem.nodeName }}></span>
      </div>
      <div v-else>
        <span v-if="elem.nodeType === 1">
          <span class="xml-tree-tag">&lt;{{ elem.nodeName }}</span>
          <span v-if="elem.hasAttributes()">
              <span v-for="(attribute, index) in elem.attributes" :key="index">
              <span class="xml-tree-attr">&nbsp;{{attribute.name}}</span>
              <span>=</span>
              <span class="xml-tree-attr">"{{attribute.value}}"</span>
              </span>
          </span>
          <span class="xml-tree-tag">></span>
          <span v-if="show"
              @click="show=false"
              style="cursor:pointer"
            >
            <slot name="hide">-</slot>
          </span>
          <span v-else
              @click="show=true"
              style="cursor:pointer"
            >
            <slot name="expand">+</slot>
          </span>
        </span>

        <div v-if="show">
          <span v-if="elem.nodeType === 3">
            {{ elem.data.trim() }}
          </span>

          <div v-for="(value, index) in children" :key="index">
              <v-xml-tree :element="value">
                <template v-slot:expand>
                <slot name="expand" />
              </template>
              <template v-slot:hide>
                <slot name="hide" />
              </template>
              <template v-slot:more>
                <slot name="more" />
              </template>
              </v-xml-tree>
          </div>
        </div>
        <slot name="more" v-else>...</slot>
        <span v-if="elem.nodeType === 1">
            <span class="xml-tree-tag">&lt;/{{ elem.nodeName }}></span>
        </span>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "vXmlTree",
  props: {
    xmlData: String,
    element: {
      type: [Element, Text],
      default: undefined
    }
  },
  computed: {
    elem() {
      if (this.element) {
        return this.element
      } else {
        const parser = new DOMParser();
        const xmlDoc = parser.parseFromString(this.xmlData, "text/xml");
        return xmlDoc.documentElement
      }
    },
    children() {
      let children = [];
      let node = this.elem.firstChild;
      while (node) {
        children.push(node);
        node = node.nextSibling;
      }

      return children;
    },
    isText() {
      if (this.children.length == 1) {
        if (this.children[0].nodeType == 3) {
           return true;
        }
      }

      return false;
    }
  },
  data() {
    return {
      show: true
    };
  }
}
</script>

<style>
</style>
