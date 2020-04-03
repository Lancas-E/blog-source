---
title: 可配置的表单
date: 2020-04-02 18:32:27
---
<link href="../dynamic-form/static/css/2.5824c4a0.chunk.css" rel="stylesheet">
<link href="../dynamic-form/static/css/main.d29bb9e6.chunk.css" rel="stylesheet">
<style>
    #root {
        margin:15px;
        padding:10px;
        width:500px;
        height:500px;
        border:1px solid grey;
        transform:translateX(0px);"
    }
    #root ul {
        margin: 0
    }
    #root .dynamic-form .next-menu {
        height: 200px
    }
</style>

表单是常见的场景，很多前端库都实现了强大的表单组件，但是我们还是发现面对大量表单会出现大量重复性工作。因此我们尝试用一种可配置的方式来实现表单(基于@alifd/next组件库)。
除了表单全局的一些设置，表单元素的核心有两点：layout和data。
- layout控制每个元素的位置，我们可以通过拖拽的方式可视化的配置表单；
- data包含每个元素的各类属性，除了沿用FormItem组件的props，对于表单元素的事件联动也在此处理；

下面的demo是data的一个实现(不考虑layout部分)，Input与Select元素可用；
性别下拉中mock生成一些数字，选中1时，会清空姓名栏，可以在元素添加事件中设置。
<div id="root"></div>

 <script>!function (e) { function r(r) { for (var n, f, i = r[0], l = r[1], a = r[2], p = 0, s = []; p < i.length; p++)f = i[p], Object.prototype.hasOwnProperty.call(o, f) && o[f] && s.push(o[f][0]), o[f] = 0; for (n in l) Object.prototype.hasOwnProperty.call(l, n) && (e[n] = l[n]); for (c && c(r); s.length;)s.shift()(); return u.push.apply(u, a || []), t() } function t() { for (var e, r = 0; r < u.length; r++) { for (var t = u[r], n = !0, i = 1; i < t.length; i++) { var l = t[i]; 0 !== o[l] && (n = !1) } n && (u.splice(r--, 1), e = f(f.s = t[0])) } return e } var n = {}, o = { 1: 0 }, u = []; function f(r) { if (n[r]) return n[r].exports; var t = n[r] = { i: r, l: !1, exports: {} }; return e[r].call(t.exports, t, t.exports, f), t.l = !0, t.exports } f.m = e, f.c = n, f.d = function (e, r, t) { f.o(e, r) || Object.defineProperty(e, r, { enumerable: !0, get: t }) }, f.r = function (e) { "undefined" != typeof Symbol && Symbol.toStringTag && Object.defineProperty(e, Symbol.toStringTag, { value: "Module" }), Object.defineProperty(e, "__esModule", { value: !0 }) }, f.t = function (e, r) { if (1 & r && (e = f(e)), 8 & r) return e; if (4 & r && "object" == typeof e && e && e.__esModule) return e; var t = Object.create(null); if (f.r(t), Object.defineProperty(t, "default", { enumerable: !0, value: e }), 2 & r && "string" != typeof e) for (var n in e) f.d(t, n, function (r) { return e[r] }.bind(null, n)); return t }, f.n = function (e) { var r = e && e.__esModule ? function () { return e.default } : function () { return e }; return f.d(r, "a", r), r }, f.o = function (e, r) { return Object.prototype.hasOwnProperty.call(e, r) }, f.p = "/"; var i = this.webpackJsonpzdynamicform = this.webpackJsonpzdynamicform || [], l = i.push.bind(i); i.push = r, i = i.slice(); for (var a = 0; a < i.length; a++)r(i[a]); var c = l; t() }([])</script>
<script src="../dynamic-form/static/js/2.0ddd061c.chunk.js"></script>
<script src="../dynamic-form/static/js/main.f4933713.chunk.js"></script>