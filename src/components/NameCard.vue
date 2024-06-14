<script setup>
import copyIcon from "./icons/copy.vue";
import whois from "./icons/whois.vue";
const props = defineProps(["domain", "tld"]);
</script>
<template>
  <li>
    {{ props.domain }}.{{ tld }}
    <span>
      <copyIcon />
      <a
        target="_blank"
        :href="'https://www.whois.com/whois/' + props.domain + '.'+ props.tld"
      >
        <whois />
      </a>
    </span>
  </li>
</template>

<style>
li {
  list-style: none;
  padding: 5px 8px;
  color: var(--vt-c-indigo);
  margin: 10px;
  border-radius: 5px;
  border: 1px solid var(--vt-c-indigo);

  display: flex;
  align-items: center;
  justify-content: space-between;
}
svg {
  cursor: pointer;
  margin: 0 5px;
}
</style>