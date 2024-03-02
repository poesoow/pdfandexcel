<script setup>
import { jsPDF } from "jspdf";

// 한글 미지원 ttf => base64 변환
import _fontmargun from '../../assets/margun.base64'

// Default export is a4 paper, portrait, using millimeters for units
const doc = new jsPDF();

doc.addFileToVFS('malgun.ttf', _fontmargun);  //_fonts 변수는 Base64 형태로 변환된 내용입니다.
doc.addFont('malgun.ttf','malgun', 'normal');
doc.setFont('malgun');

doc.text("한글", 10, 10);
doc.save("a4.pdf");

const doc2 = new jsPDF({
  orientation: "landscape",
  unit: "in",
  format: [4, 2]
})

doc2.text("한글2", 1, 1);
doc2.save("two-by-four.pdf");
</script>

<template>
  <div>dd</div>
</template>

<style scoped>
.read-the-docs {
  color: #888;
}
</style>
