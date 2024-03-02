<script setup>
import { jsPDF } from "jspdf";
import autoTable from 'jspdf-autotable'

// 한글 미지원 ttf => base64 변환
import _fontmargun from '../../assets/margun.base64'

// Default export is a4 paper, portrait, using millimeters for units
const doc = new jsPDF();

doc.addFileToVFS('malgun.ttf', _fontmargun);  //_fonts 변수는 Base64 형태로 변환된 내용입니다.
doc.addFont('malgun.ttf','malgun', 'normal');
doc.setFont('malgun');

//// It can parse html:
//// <table id="my-table"><!-- ... --></table>
// autoTable(doc, { html: '#my-table' })

// Or use javascript directly:
autoTable(doc, {
  styles: { fillColor: [255, 0, 0] },
  columnStyles: { 0: { halign: 'center', fillColor: [0, 255, 0] } }, // Cells in first column centered and green
  margin: { top: 10 },
  head: [['Name', 'Email', 'Country']],
  body: [
    ['David', 'david@example.com', 'Sweden'],
    ['Castille', 'castille@example.com', 'Spain'],
    ['David', 'david@example.com', 'Sweden'],
    ['Castille', 'castille@example.com', 'Spain'],
    ['David', 'david@example.com', 'Sweden'],
    ['Castille', 'castille@example.com', 'Spain'],
    ['David', 'david@example.com', 'Sweden'],
    ['Castille', 'castille@example.com', 'Spain'],
    ['David', 'david@example.com', 'Sweden'],
    ['Castille', 'castille@example.com', 'Spain'],
    ['David', 'david@example.com', 'Sweden'],
    ['Castille', 'castille@example.com', 'Spain'],
    ['David', 'david@example.com', 'Sweden'],
    ['Castille', 'castille@example.com', 'Spain'],
    ['David', 'david@example.com', 'Sweden'],
    ['Castille', 'castille@example.com', 'Spain'],
    ['David', 'david@example.com', 'Sweden'],
    ['Castille', 'castille@example.com', 'Spain'],
    ['David', 'david@example.com', 'Sweden'],
    ['Castille', 'castille@example.com', 'Spain'],
    ['David', 'david@example.com', 'Sweden'],
    ['Castille', 'castille@example.com', 'Spain'],
    ['David', 'david@example.com', 'Sweden'],
    ['Castille', 'castille@example.com', 'Spain'],
    ['David', 'david@example.com', 'Sweden'],
    ['Castille', 'castille@example.com', 'Spain'],
    ['David', 'david@example.com', 'Sweden'],
    ['Castille', 'castille@example.com', 'Spain'],
    ['David', 'david@example.com', 'Sweden'],
    ['Castille', 'castille@example.com', 'Spain'],
    ['David', 'david@example.com', 'Sweden'],
    ['Castille', 'castille@example.com', 'Spain'],
    ['David', 'david@example.com', 'Sweden'],
    ['Castille', 'castille@example.com', 'Spain'],
    ['David', 'david@example.com', 'Sweden'],
    ['Castille', 'castille@example.com', 'Spain'],
    ['David', 'david@example.com', 'Sweden'],
    ['Castille', 'castille@example.com', 'Spain'],
    ['David', 'david@example.com', 'Sweden'],
    ['Castille', 'castille@example.com', 'Spain'],
    ['David', 'david@example.com', 'Sweden'],
    ['Castille', 'castille@example.com', 'Spain'],
    // ...
  ],
})



doc.save("table.pdf");
</script>

<template>
  <div>
    <table id="my-table">
  <tr>
    <th>이름</th>
    <th>직업</th>
    <th>나이</th>
  </tr>
  <tr>
    <td>홍길동</td>
    <td>의사</td>
    <td>35세</td>
  </tr>
  <tr>
    <td>김철수</td>
    <td>교사</td>
    <td>28세</td>
  </tr>
  <tr>
    <td>이영희</td>
    <td>회사원</td>
    <td>30세</td>
  </tr>
</table>
  </div>
</template>

<style scoped>
.read-the-docs {
  color: #888;
}
</style>
