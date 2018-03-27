<template>
  <Page class="page">
    <ActionBar class="action-bar" title="Hello world">
    </ActionBar>

    <StackLayout class="hello-world">
      <Label class="body" textWrap=true text="This is a hello world component, tap the button if you dare"/>

      <Button class="btn btn-primary" @tap="surprise = !surprise" text="Tap me!"/>
      <Button class="btn btn-primary" @tap="printRandomBytes" text="Print randomBytes"/>
      <Image v-if="surprise" src="~/images/NativeScript-Vue.png"/>

      <Label class="body" textWrap=true :text="'Value:' + xValue"/>
      <web-view ref="webView" v-show="false"></web-view>

    </StackLayout>

  </Page>
</template>

<script>
import webViewInterfaceModule from "nativescript-webview-interface";
var oWebViewInterface;
export default {
  data() {
    return {
      surprise: false,
      xValue: 10
    };
  },
  mounted() {
    var webView = this.$refs.webView.nativeView;
    oWebViewInterface = new webViewInterfaceModule.WebViewInterface(
      webView,
      "~/www/index.html"
    );
  },
  methods: {
    printRandomBytes() {
      oWebViewInterface.callJSFunction("getRandomBytes", 24, result => {
        this.xValue = result.data;

      });
    }
  }
};
</script>

<style scoped>
.hello-world {
  margin: 20;
}

Label {
  color: red;
}
</style>
