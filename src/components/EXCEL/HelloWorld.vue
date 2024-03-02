<script setup>
import * as Excel from "exceljs/dist/exceljs.min.js";
import { saveAs } from "file-saver";

// 데이터 배열
const list = [
  {
    orderNum: "A309012",
    menu: "햄버거",
    price: 12000,
    date: "2023-05-01",
  },
  {
    orderNum: "B882175",
    menu: "아메리카노(ice)",
    price: 1900,
    date: "2023-05-17",
  },
  {
    orderNum: "B677919",
    menu: "떡볶이",
    price: 6000,
    date: "2023-05-28",
  },
  {
    orderNum: "A001092",
    menu: "마라탕",
    price: 28000,
    date: "2023-06-12",
  },
  {
    orderNum: "A776511",
    menu: "후라이드치킨",
    price: 18000,
    date: "2023-06-12",
  },
  {
    orderNum: "A256512",
    menu: "고급사시미",
    price: 289900,
    date: "2023-06-12",
  },
  {
    orderNum: "C114477",
    menu: "단체도시락",
    price: 1000000,
    date: "2023-06-19",
  },
];

// TH에 들어갈 텍스트 데이터
const headers = ["주문번호", "메뉴", "가격", "주문날짜"];
// TH width, 단위는 cell의 width나 height 단위는 픽셀이 아닌 엑셀의 너비 기준이다.
const headerWidths = [40, 16, 16, 24];

const downloadList = async (rows) => {
    try {
      //console.log(rows);

			// workbook 생성
      const wb = new Excel.Workbook();
			// sheet 생성
      const sheet = wb.addWorksheet("배달 주문 내역");

      // 상단 헤더(TH) 추가
      const headerRow = sheet.addRow(headers);
      // 헤더의 높이값 지정
      headerRow.height = 30.75;
      // 각 헤더 cell에 스타일 지정
      headerRow.eachCell((cell, colNum) => {
        styleHeaderCell(cell);
        sheet.getColumn(colNum).width = headerWidths[colNum - 1];
      });

      // 각 Data cell에 데이터 삽입 및 스타일 지정
      rows.forEach(({ orderNum, menu, price, date }) => {
        const rowDatas = [orderNum, menu, price, date];
        const appendRow = sheet.addRow(rowDatas);

        appendRow.eachCell((cell, colNum) => {
          styleDataCell(cell, colNum);
          if (colNum === 1) {
            cell.font = {
              color: { argb: "ff1890ff" },
            };
          }
          if (colNum === 3) {
            cell.numFmt = "0,000";
          }
        });
      });

      // 파일 생성
      const fileData = await wb.xlsx.writeBuffer(); //writeBuffer는 프로미스를 반환하므로 async-await을 사용해야 한다.
      const blob = new Blob([fileData], {
        type: "application/vnd.openxmlformats-officedocument.spreadsheetml.sheet",
      });
      saveAs(blob, `배달 주문 내역`);
    } catch (error) {
      console.log(error);
    }
  }

  const styleHeaderCell = (cell) => {
  cell.fill = {
    type: "pattern",
    pattern: "solid",
    fgColor: { argb: "ffebebeb" },
  };
  cell.border = {
    bottom: { style: "thin", color: { argb: "-100000f" } },
    right: { style: "thin", color: { argb: "-100000f" } },
  };
  cell.font = {
    name: "Arial",
    size: 12,
    bold: true,
    color: { argb: "ff252525" },
  };
  cell.alignment = {
    vertical: "middle",
    horizontal: "center",
    wrapText: true,
  };
};

const styleDataCell = (cell) => {
  cell.fill = {
    type: "pattern",
    pattern: "solid",
    fgColor: { argb: "ffffffff" },
  };
  cell.border = {
    bottom: { style: "thin", color: { argb: "-100000f" } },
    right: { style: "thin", color: { argb: "-100000f" } },
  };
  cell.font = {
    name: "Arial",
    size: 10,
    color: { argb: "ff252525" },
  };
  cell.alignment = {
    vertical: "middle",
    horizontal: "center",
    wrapText: true,
  };
};
</script>

<template>
  <div>
    <button @click="downloadList(list)">엑셀 추출</button>
    {{ list }}
  </div>
</template>

<style scoped>
.read-the-docs {
  color: #888;
}
</style>
