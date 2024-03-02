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

// Example usage of columns property. Note that America will not be included even though it exist in the body since there is no column specified for it.
autoTable(doc, {
  headStyles:  { halign: 'center', valign: 'middle' },  //헤더 부분 옵션
    startX: 1, // 시작x좌표
    startY: 1, // 시작y좌표
    // margin: {  left : 왼쪽, top : 위, right : 오른쪽  },  //여백
    // tableWidth : 테이블넓이,
    styles : { font : 'malgun', fontStyle :'normal'},  //폰트적용
    head: [['헤더1', '헤더2', '헤더3']],
    body : [
        [
            {content: '데이터1', rowSpan: 2, styles: {halign: 'center', valign: 'middle'}},  //여러 속성들, content는 내용입니다.
            {content: '데이터2', styles: {halign: 'center', fillColor: [ 252, 252, 252 ]}},
            {content: '데이터3', styles: {halign: 'center'}},
        ],
        [
            {content: '데이터4', styles: {halign: 'center', fillColor: [ 252, 252, 252 ]}},
            {content: '데이터5', styles: {halign: 'center'}},
        ]
    ]
})

doc.save("table.pdf");
</script>

<template>
  <div>
    ddd
  </div>
</template>

<style scoped>
.read-the-docs {
  color: #888;
}
</style>
