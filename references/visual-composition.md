# 内容构图与 SVG 图解

在需要表达结构关系、或改善整套设计节奏时使用。固定母版与字号规则见主 skill；这些构图是选择依据，不是必须逐个使用的版式库。

## 用关系选择主视觉

| 表达任务 | 可用构图 | 阅读路径与判断依据 |
| --- | --- | --- |
| 自动化机制 | 跨泳道流程、分支与回路 | 沿箭头读输入到输出；人、AI、系统的位置表达责任边界 |
| 变化前后 | 两条共享起终点的路径 | 对齐同一比较维度，突出减少的交接或保留的人工判断；不虚构耗时 |
| 分类与归属 | 偏置树状图、局部展开的分支 | 从总类到子类；展示足以说明结构的分支，其余用真实汇总标签 |
| 依赖与能力层次 | 错落叠层、剖面与括注 | 从基础到应用；层高不编码未经证实的能力大小 |
| 演进或计划 | 折线路径、里程碑带、上下交替注释 | 沿明确顺序读；等距步骤不冒充按时间比例绘制的轴 |
| 多维比较 | 有共享列标题的矩阵、配对点线 | 对齐维度后再表达差异；长说明留在讲者备注 |
| 核心判断 | 单一主体图解配短结论、偏置文字构图 | 留白集中注意力；保持正文与标题字号，不靠超大口号制造变化 |

先明确图中的节点、边和分组各代表什么，再选择形状。闭环只用于反馈，树状只用于归属，箭头用于真实方向；不用圆环、漏斗或网络形状替代不存在的逻辑。SVG 可以是全页主体，也可以与局部文本或表格组合。若一句话已足够清楚，直接排文字。

整套节奏来自结构差异：同一品牌下，既有关系图，也有精确比较、案例局部或简短判断。连续比较允许相同骨架。审阅时忽略文案和颜色，若不同任务页面仍只剩同样的矩形阵列，重做主体。

## SVG 与 HTML 协作

推荐将 SVG 用于结构线、箭头、分组边界和节点几何，用 HTML 排版标题与长标签。让两层共享一个有明确宽高的相对定位容器；SVG 用同宽高的 viewBox。按节点坐标对齐 HTML 标签，避免标签悬空或连接线穿字。不要分别缩放图解和标签。

```html
<div class="process-map">
  <svg viewBox="0 0 1400 460" aria-hidden="true" focusable="false">
    <defs>
      <marker id="flow-p12-arrow" viewBox="0 0 10 10"
        refX="8" refY="5" markerWidth="7" markerHeight="7" orient="auto">
        <path d="M 1 1 L 8 5 L 1 9" fill="none" stroke="var(--blue-main)" />
      </marker>
    </defs>
    <path d="M 250 230 H 600" fill="none" stroke="var(--blue-main)"
      stroke-width="3" marker-end="url(#flow-p12-arrow)"
      data-reveal="draw" pathLength="1" />
  </svg>
  <div class="process-label process-input"><h3>输入</h3><p>真实输入内容</p></div>
  <div class="process-label process-output"><h3>输出</h3><p>真实输出内容</p></div>
</div>
```

```css
.process-map { position: relative; width: 1400px; height: 460px; }
.process-map > svg { position: absolute; inset: 0; width: 100%; height: 100%; }
.process-label { position: absolute; width: 220px; }
.process-input { left: 20px; top: 180px; }
.process-output { left: 630px; top: 180px; }
```

代码仅演示几何与标签协作，不是可直接填充所有流程的模板。实际节点数量、端点和间距由内容决定。

- 线宽通常 2–4 个画布像素，主关系深蓝或主蓝，辅助边界淡灰蓝；金色保留给核心文字或局部节点。
- 内联 SVG 的 `defs` ID 使用页级前缀，避免跨页 marker 引用错位。图形与文字均不放在字号规则之外。
- 用 SVG `<text>` 时明确对应字体栈并验证实际命中；不要先做很小的 viewBox 再放大，让标签实际字号失控。多行标签优先 HTML。
- 纯几何且旁边已有完整解释时使用 `aria-hidden="true"`。图解独立承载信息时用 `role="img"`、唯一的 `<title>` / `<desc>` ID 和 `aria-labelledby`，或提供相邻等价文字。
- 引用截图时仍用 PNG，不把 SVG 当成截图或真实产品 UI；示意界面自然标明“结构示意”。

## 动效搭配

页面转场通过 `.slide` 的 `data-transition` 指定，不单独接管导航。优先选择一套连贯的动效语法，例如流程页 push、层级页 lift、章节关键图 focus，其余 fade。wipe 可用于全景或有横向阅读顺序的图，不把长段落逐字揭示。

`data-reveal` 用于少量有语义顺序的分组，`data-reveal="fade"` 用于不需要移动的标签。描线用 `data-reveal="draw" pathLength="1"`；不添加常驻流动粒子、脉冲或循环虚线。描线元素不要放在另一个 reveal 容器中，避免两层动画叠加。

所有信息在动画结束、快速反向翻页、减弱动效、静态截图和打印时保持完整。PDF 不承载动效，不能拿 PDF 作为交互验收。动画中途也检查一次主体移动与品牌位置，静态终态看不出这些问题。
