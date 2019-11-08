---
layout: post
title: javascript 로 table row 값 json으로 변경하기.
description: javascript를 이용해서 table row를 json형태로 변환하는 샘플.
categories: html css javascript
---

# javascript를 이용해서 table row를 json형태로 변환하는 샘플.

---

javascript로 table row를 json으로 변경해보았다.

# sample source

---

html, css로 구현되어 있다.

예제 소스는 아래와 같다.

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <meta http-equiv="X-UA-Compatible" content="ie=edge" />
    <title>Document</title>

    <style>
      * {
        padding: 0;
        margin: 0;
      }

      table {
        width: 80%;
        margin: 0 auto;
        border-collapse: collapse;
        text-align: left;
        line-height: 1.5;
        border: 1px solid #cccccc;
      }

      thead th {
        font-weight: bold;
        vertical-align: top;
        border-bottom: 1px solid #cccccc;
      }

      td {
        vertical-align: top;
        width: 20%;
        padding: 1% 0 1% 0;
        border-bottom: 1px solid #cccccc;
      }

      th:first-child,
      td:first-child {
        padding-left: 2%;
      }

      div:nth-child(1) {
        width: 80%;
        margin: 0 auto;
        margin-bottom: 2%;
      }

      table ~ div {
        width: 80%;
        margin: 0 auto;
        margin-top: 2%;
      }

      textarea {
        width: 100%;
      }

      .td--text {
        border: 0;
        box-shadow: none;
        background-color: transparent;
      }
      .td--text:focus {
        outline: none;
      }

      .td--text__none {
        display: none;
      }
    </style>
  </head>
  <body>
    <div>
      <button id="save">save</button>
      <button id="delete">delete</button>
      <button id="add">add</button>
    </div>

    <table>
      <thead>
        <tr>
          <th><input type="checkbox" class="all" /></th>
          <th>name</th>
          <th>weight</th>
          <th>set</th>
          <th>pick</th>
        </tr>
      </thead>

      <tbody>
        <tr>
          <td><input type="checkbox" /></td>

          <td>
            <input class="td--text__none" type="text" name="_id" value="" />
            <input class="td--text" type="text" name="name" value="push up" />
          </td>
          <td>
            <input class="td--text" type="text" name="weight" value="0" />
          </td>

          <td>
            <input class="td--text__none" type="hidden" name="set" value="0" />
            <select>
              <option>1</option>
              <option>2</option>
              <option>3</option>
              <option>4</option>
              <option selected>5</option>
            </select>
          </td>
          <td>
            <input
              class="td--checkbox"
              type="checkbox"
              name="pick"
              value="false"
            />
          </td>
        </tr>

        <tr>
          <td><input type="checkbox" /></td>
          <td>
            <input class="td--text__none" type="text" name="_id" value="" />
            <input class="td--text" type="text" name="name" value="push up" />
          </td>
          <td>
            <input class="td--text" type="text" name="weight" value="0" />
          </td>

          <td>
            <input class="td--text__none" type="hidden" name="set" value="0" />
            <select>
              <option>1</option>
              <option>2</option>
              <option>3</option>
              <option>4</option>
              <option selected>5</option>
            </select>
          </td>
          <td>
            <input
              class="td--checkbox"
              type="checkbox"
              name="pick"
              value="false"
            />
          </td>
        </tr>

        <tr>
          <td><input type="checkbox" /></td>
          <td>
            <input class="td--text__none" type="text" name="_id" value="" />
            <input class="td--text" type="text" name="name" value="push up" />
          </td>
          <td>
            <input class="td--text" type="text" name="weight" value="0" />
          </td>

          <td>
            <input class="td--text__none" type="hidden" name="set" value="0" />
            <select>
              <option>1</option>
              <option>2</option>
              <option>3</option>
              <option>4</option>
              <option selected>5</option>
            </select>
          </td>
          <td>
            <input
              class="td--checkbox"
              type="checkbox"
              name="pick"
              value="false"
            />
          </td>
        </tr>

        <tr>
          <td><input type="checkbox" /></td>
          <td>
            <input class="td--text__none" type="text" name="_id" value="" />
            <input class="td--text" type="text" name="name" value="push up" />
          </td>
          <td>
            <input class="td--text" type="text" name="weight" value="0" />
          </td>
          <td>
            <input class="td--text__none" type="hidden" name="set" value="0" />
            <select>
              <option>1</option>
              <option>2</option>
              <option>3</option>
              <option>4</option>
              <option selected>5</option>
            </select>
          </td>
          <td>
            <input
              class="td--checkbox"
              type="checkbox"
              name="pick"
              value="false"
            />
          </td>
        </tr>
      </tbody>
    </table>
    <div>
      <textarea id="result" cols="70" rows="20"> </textarea>
    </div>
  </body>
  <script>
    document.querySelector("#save").addEventListener("click", function() {
      const checkedBoxes = document.querySelectorAll(
        "input:checked:not(.all):not(.td--checkbox)"
      );
      const checkedRows = Array.prototype.slice.call(checkedBoxes);
      const cols = checkedRows.map(function(element) {
        const rows = Array.prototype.slice.call(
          element.closest("tr").children,
          1
        );

        const objs = rows.reduce(function(result, item, index) {
          const obj = {};

          let element = item.firstElementChild;
          obj[element.name] = element.value;

          while (
            (element = element.nextElementSibling) != null &&
            element.tagName !== "SELECT"
          ) {
            obj[element.name] = element.value;
          }

          return {
            ...obj,
            ...result
          };
        }, {});
        return objs;
      });

      const textarea = document.querySelector("#result");
      textarea.value = JSON.stringify(cols);
    });

    document
      .querySelector("#delete")
      .addEventListener("click", function(target) {});

    document.querySelector("#add").addEventListener("click", function(target) {
      const tableBody = document.querySelector("table tbody");
      tableBody.insertAdjacentHTML("beforeend", '<tr>\
          <td><input type="checkbox" /></td> \
          <td>\
           <input class="td--text__none" type="text" name="_id" value="" />\
           <input class="td--text" type="text" name="name" value="" />\
          </td>\
          <td>\
           <input class="td--text" type="text" name="weight" value="" />\
          </td>\
           <td> \
             <input class="td--text__none" type="hidden" name="set" value="" />\
             <select> \
              <option selected>1</option> \
              <option>2</option> \
              <option>3</option> \
              <option>4</option> \
              <option>5</option> \
             </select>\
           </td>\
          <td>\
            <input \
              class="td--checkbox" \
              type="checkbox"\
              name="pick"\
              value="false"\
            />\
          </td>\
        </tr>');
    });

    document
      .querySelector("table tbody")
      .addEventListener("change", function(event) {
        const target = event.target;

        if (!target || target.nodeName !== "SELECT") {
          return;
        }
        const value = target.previousElementSibling;
        value.value = target.value;
      });

    document
      .querySelector("input[type=checkbox]:first-child")
      .addEventListener("click", function(event) {
        const checked = event.target.checked;
        const checkboxes = document.querySelectorAll(
          "input[type=checkbox]:not(.all):not(.td--checkbox)"
        );
        checkboxes.forEach(function(element) {
          element.checked = checked;
        });
      });

    document.querySelectorAll(".td--checkbox").forEach(function(element) {
      element.addEventListener("change", function(target) {
        if (this.checked) {
          this.value = true;
        } else {
          this.value = false;
        }
      });
    });
  </script>
</html>
```
