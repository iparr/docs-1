<template>
    <a
      class="since" 
      :href="releaseUrl"
      :title="`${feature} was first available in version ${ver} of Craft.`"
      target="_blank">
        {{ ver }}<span class="plus">+</span>
      </a>
</template>

<script>
const GITHUB_URL = "https://github.com";
const GITHUB_CHANGELOG_FILENAME = "CHANGELOG.md";

export default {
  components: {},
  props: {
    ver: String,
    useChangelog: {
      type: Boolean,
      default: true,
    },
    repo: {
      type: String,
      default: 'craftcms/cms',
    },
    feature: {
      type: String,
      default: 'This feature',
    },
  },
  computed: {
    releaseUrl() {
      // We started supporting GitHub releases in 4.4.6 and 3.8.7. This doesn't validate the incoming version number. Check your references for dead URLs!
      if (this.useChangelog) {
        return `${GITHUB_URL}/${this.repo}/blob/${this.ver}/${GITHUB_CHANGELOG_FILENAME}`;
      }

      return `${GITHUB_URL}/${this.repo}/releases/tag/${this.ver}`;
    },
  },
};
</script>

<style lang="postcss" scoped>
.since {
  @apply inline-block rounded-md py-1 px-1;
  background-color: var(--custom-block-bg-color);
  border-color: var(--custom-block-border-color);
  font-size: 13px;
  vertical-align: super;
  line-height: 12px;

  &:hover {
    background-color: var(--code-bg-color);
    text-decoration: none;
  }
}
</style>
