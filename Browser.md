# Browser

## Index of Contents

- Script
- Model
- Event
- Dom
- Render Process
  - Repaint
  - Reflow

## Script

- defer
  - Not every browser exec script with defer attribute in the last one.
  - Load script and parse document simultaneously and load the script after the document has been pared.
- async
  - Async load script and execute immediately if document has not yet been pared. Otherwise, the script will be blocked until document has been pared.
  - Order is not predictable when loading multiple scripts with async
- Dynamically create DOM
  - e.g. Load JS after document.onload
- setTimeout
- Load JS after main context

## Model

### Web API - Performance

#### 如何在 H5 和小程序项目中计算白屏时间和首屏时间

白屏时间: 第一個元素出現
首屏时间: 第一屏喧染完成
Ref. [Web 性能优化-首屏和白屏时间](https://lz5z.com/Web%E6%80%A7%E8%83%BD%E4%BC%98%E5%8C%96-%E9%A6%96%E5%B1%8F%E5%92%8C%E7%99%BD%E5%B1%8F%E6%97%B6%E9%97%B4/)

## Event

## Dom

## Cookie & Token

## Render Process

### Repaint

### Reflow
