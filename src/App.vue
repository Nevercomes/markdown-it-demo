<template>
  <div id="app">
    <h1>Markdown + TeXMath Demo</h1>
    <textarea v-model="input" placeholder="Type markdown with TeXmath here..." />
    <div v-html="renderedMarkdown" class="markdown-content"></div>
  </div>
</template>

<script>
import MarkdownIt from "markdown-it";
import texmath from "markdown-it-texmath";
import "katex/dist/katex.min.css";

export default {
  data() {
    return {
      /* eslint-disable no-useless-escape */
      input: String.raw`### Dollar
$a^2+b^2=c^2$

$$a^2+b^2=c^2$$

$$
a^2+b^2=c^2
$$

$$\text{Cl}_2 + \text{S}^{2-} = \text{S}↓ + 2\text{Cl}^-$$


### Bracket

\(a^2+b^2=c^2\)

\[a^2+b^2=c^2\]

\[
a^2+b^2=c^2
\]

\[\text{Cl}_2 + \text{S}^{2-} = \text{S}↓ + 2\text{Cl}^-\]
`,
      md: null,
    };
  },
  computed: {
    renderedMarkdown() {
      return this.md.render(this.input);
    },
  },
  created() {
    this.md = new MarkdownIt().use(texmath, {
      engine: require("katex"),
      delimiters: ["dollars", "brackets"],
    });
  },
};
</script>

<style>
.markdown-content {
  border: 1px solid #ddd;
  padding: 1em;
  margin-top: 1em;
}
textarea {
  width: 100%;
  height: 150px;
  margin-bottom: 1em;
}
</style>
