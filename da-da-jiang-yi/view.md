# View

### 元件**的大致分類**

<table>
  <thead>
    <tr>
      <th style="text-align:left"><b>View</b>
      </th>
      <th style="text-align:left"><b>ViewGroup</b>
      </th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">
        <p></p>
        <ul>
          <li><b>TextView</b>
          </li>
          <li><b>ImageView</b>
          </li>
          <li><b>EditText</b>
          </li>
          <li><b>etc...</b>
          </li>
        </ul>
      </td>
      <td style="text-align:left">
        <p></p>
        <ul>
          <li><b>FrameLayout</b>
          </li>
          <li><b>LinearLayout</b>
          </li>
          <li><b>ScrollView</b>
          </li>
          <li><b>ConstraintLayout</b>
          </li>
          <li><b>etc...</b>
          </li>
        </ul>
      </td>
    </tr>
  </tbody>
</table>

### **View常用Attribute**

<table>
  <thead>
    <tr>
      <th style="text-align:left"><b>View(&#x6240;&#x6709;&#x5176;&#x4ED6;&#x5143;&#x4EF6;&#x90FD;&#x6703;&#x7528;&#x5230;)</b>
      </th>
      <th style="text-align:left"><b>TextView</b>
      </th>
      <th style="text-align:left"><b>ImageView</b>
      </th>
      <th style="text-align:left"><b>EditText</b>
      </th>
      <th style="text-align:left"><b>LinearLayout</b>
      </th>
      <th style="text-align:left"><b>FrameLayout</b>
      </th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">
        <ul>
          <li><b>id</b>
          </li>
          <li><b>layout_width</b>
          </li>
          <li><b>layout_height</b>
          </li>
          <li><b>background</b>
          </li>
          <li><b>padding</b>
          </li>
          <li><b>visibility</b>
          </li>
        </ul>
      </td>
      <td style="text-align:left">
        <p></p>
        <ul>
          <li><b>text</b>
          </li>
          <li><b>textColor</b>
          </li>
          <li><b>textSize</b>
          </li>
        </ul>
      </td>
      <td style="text-align:left"><b>srcCompat</b>
      </td>
      <td style="text-align:left">
        <p></p>
        <ul>
          <li><b>inputType</b>
          </li>
          <li><b>ems</b>
          </li>
        </ul>
      </td>
      <td style="text-align:left"><b>orientation</b>
      </td>
      <td style="text-align:left"></td>
    </tr>
  </tbody>
</table>

### **ScrollView**

* **必定是由ScrollView + LinearLayout\(Vertical\) 組成**
* **將想要滑動的畫面放到LinearLayout當中**

### **ConstraintLayout**

<table>
  <thead>
    <tr>
      <th style="text-align:left"><b>&#x57FA;&#x672C;&#x7528;&#x6CD5;</b>
      </th>
      <th style="text-align:left"><b>&#x9032;&#x968E;&#x7528;&#x6CD5;</b>
      </th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">
        <ul>
          <li><b>Relative positioning</b>
          </li>
          <li><b>Margins</b>
          </li>
          <li><b>Centering positioning</b>
          </li>
          <li><b>Dimension constraints</b>
          </li>
          <li><b>Chains</b>
          </li>
          <li><b>Virtual Helpers objects</b>
            <ul>
              <li><b>Guideline</b>
              </li>
              <li><b>Group</b>
              </li>
            </ul>
          </li>
        </ul>
      </td>
      <td style="text-align:left">
        <ul>
          <li><b>Virtual Helpers objects</b>
            <ul>
              <li><b>Barrier</b>
              </li>
              <li><b>Layer</b>
              </li>
              <li><b>Flow</b>
              </li>
            </ul>
          </li>
          <li><b>Circular positioning</b>
          </li>
          <li><b>Visibility</b>
          </li>
          <li><b>Optimizer</b>
          </li>
        </ul>
      </td>
    </tr>
  </tbody>
</table>

### **與程式碼的互動**

* **findViewById&lt;T extend View&gt;\(\)**
* [**viewbinding**](https://developer.android.com/topic/libraries/view-binding)
* [**setOnClickListener**](https://developer.android.com/reference/android/view/View.OnClickListener)

