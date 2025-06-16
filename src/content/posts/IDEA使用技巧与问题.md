---
title: IDEA使用技巧与问题
author: Francisco
description: 解决MybatisX报错的方法包括自定义yml文件依赖和插件推荐，如CamelCase、CodeGlance Pro和JRebel等，提升代码效率和调试体验。
pubDate: 2025-01-12
categories: ["IDEA"]
slug: when-npx-creates-project-error
pin: false
---

![](https://s2.loli.net/2025/06/12/fBMFzXCEV8jOZam.png)

# **技巧**

## **解决MybatisX statement 报错**

问题现状

![](https://s2.loli.net/2025/06/12/YijLAn9JDCWM1cS.png)

解决方案

![](https://s2.loli.net/2025/06/12/QpN68ECtD1cH9AL.png)

![](https://s2.loli.net/2025/06/12/vWsXcomxzq8wL6Y.png)

![](https://s2.loli.net/2025/06/12/7SIMl59DzJk6naR.png)

## **yam文件自定义警告依赖**

```xml
<!--yml配置文件自适应-->
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-configuration-processor</artifactId>
    <optional>true</optional>
</dependency>
```

## **MybatisX插件自动生成图选项**

![](https://s2.loli.net/2025/06/12/rLGCf6Hjtcw78vm.png)

# 插件推荐

### **CamelCase**

将驼峰命名自动转换为下划线或其他命名风格，支持双击选中整个变量名称的一部分，提升代码导航与编辑效率。

---

### **CodeGlance Pro**

在编辑器右侧显示迷你代码地图，类似 VSCode 的代码预览功能，方便快速定位代码结构和热点区域。

---

### **Generate All Getter And Setter**

一键为类中的所有字段生成 Getter 和 Setter 方法，节省大量样板代码的手动编写时间。

---

### **GitHub Dark Theme**

为 IDEA 提供 GitHub 样式的深色主题，视觉上更舒适，适合长时间编码。

---

### **JRebel and XRebel**

用于 Java 热部署和性能分析，JRebel 支持无需重启即可实时加载代码变更，XRebel 提供性能监控和慢查询分析，常用于 Spring Boot 开发。

---

### **Maven Helper**

图形化查看和分析 Maven 项目依赖关系，支持查找冲突依赖、快速跳转依赖源，解决依赖版本问题更高效。

---

### **MyBatis Log**

自动提取控制台中的 MyBatis SQL 日志，并高亮显示完整的 SQL 语句和参数绑定，方便调试和优化 SQL。

---

### **MybatisX-ext**

MyBatis Plus 的辅助插件，支持从 Mapper 跳转到 XML 文件、方法预览 SQL 等，极大提升开发效率，适用于重度 MyBatis 用户。

---

### **Naming Is Hard**

起名困难症福音插件，提供有趣、语义化的变量名建议，自动生成更具意义的变量命名。

---

### **Rainbow Brackets**

为代码中的括号上色，尤其适合阅读嵌套结构复杂的代码，防止漏看括号或理解错误。

---
