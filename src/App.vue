<template>
  <ejs-treegrid ref="treegrid" :dataSource="data" childMapping="subtasks" 
    :treeColumnIndex="1" :height='450' :allowPaging="true"
    :allowPdfExport="true" :toolbar="toolbarOptions" :toolbarClick="toolbarBtnClick">
    <e-columns>
        <e-column field='ID' headerText='S.No' width='90' textAlign='Right'></e-column>
        <e-column field='Name' headerText='ShipMent Name' width='220'></e-column>
        <e-column field='category' headerText='Category' width='220'></e-column>
        <e-column field='unitPrice' headerText='Unit Price($)' format='c2' width='120' textAlign='Right'></e-column>
        <e-column field='price' headerText='Price($)' width='100' format='c' textAlign='Right'></e-column>
    </e-columns>
  </ejs-treegrid>
</template>
<script>
import { TreeGridComponent, ColumnsDirective, ColumnDirective, Page, PdfExport, Toolbar } from "@syncfusion/ej2-vue-treegrid";
import {summaryData} from './data.js';

export default{
  name: 'App',
  components: {
    'ejs-treegrid': TreeGridComponent,
    'e-columns': ColumnsDirective,
    'e-column': ColumnDirective
  },
  data: () => {
    return {
      data: summaryData,
      toolbarOptions: ['PdfExport']
    }
  },
  methods:{
    toolbarBtnClick:function(args){
      var treegridObj = this.$refs.treegrid.ej2Instances;
      if(args['item'].text ==='PDF Export'){
        treegridObj.pdfExport({
          fileName: "SummaryData.pdf",
          theme:{
            header:{
              fontColor: "#64FA50",
              fontName: "Calibri",
              fontSize: 10,
              bold: true
            },
            record:{
              fontSize: 8,
              fontName: "Calibri",
              fontColor: "#0000FF"
            }
          },
          header:{
            fromTop: 0,
            height: 130,
            contents: [
              {
                type: "Text",
                value: "Shipment Details",
                position: {x:0, y:50},
                style:{fontSize:20}
              }
            ]
          },
          footer:{
            fromBottom: 130,
            height: 130,
            contents:[
              {
                type: 'Line',
                style: {penColor:"#000080", penSize:2, dashStyle:"Solid"},
                points: { x1: 0, y1: 4, x2: 685, y2: 4}
              }
            ]
          }
        });
      }
    }
  },
  provide:{
    treegrid: [Page, PdfExport, Toolbar]
  }
}
</script>

<style>
  @import "../node_modules/@syncfusion/ej2-base/styles/material.css";
  @import "../node_modules/@syncfusion/ej2-buttons/styles/material.css";
  @import "../node_modules/@syncfusion/ej2-calendars/styles/material.css";
  @import "../node_modules/@syncfusion/ej2-dropdowns/styles/material.css";
  @import "../node_modules/@syncfusion/ej2-inputs/styles/material.css";
  @import "../node_modules/@syncfusion/ej2-navigations/styles/material.css";
  @import "../node_modules/@syncfusion/ej2-popups/styles/material.css";
  @import "../node_modules/@syncfusion/ej2-splitbuttons/styles/material.css";
  @import "../node_modules/@syncfusion/ej2-vue-grids/styles/material.css";
  @import "../node_modules/@syncfusion/ej2-vue-treegrid/styles/material.css";
</style>
