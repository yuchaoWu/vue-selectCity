<!-- 城市选择组件 -->
<template>
    <div id="SelectCity">
        <el-form :model="form" :rules="rules" ref="form" label-width="80px">
            <el-form-item label="所在地区" prop="areaList">
                <el-input v-model="form.areaList" style="width:60%;" disabled></el-input>
                <el-button @click="dialogVisible = true">选择</el-button>
            </el-form-item>
            <!--选择地区弹窗开始-->
            <el-dialog :visible.sync="dialogVisible" top="6%" size="large">
                <el-form :model="dialogForm" label-width="80px" ref="dialogForm">
                    <el-row>
                        <el-col :span="24">
                            <el-form-item label="已选区域" prop="selectedArea">
                                <el-tag style="margin-left: 10px"
                                        v-for="item in dialogForm.selectedArea"
                                        :key="item.value"
                                >{{item.label}}</el-tag>
                            </el-form-item>
                            <el-form-item label="选择省份" prop="provinces">
                                <el-checkbox-group v-model="dialogForm.provinces"  @change="checkedProvince">
                                    <template v-for="item in provinceOptions">
                                        <el-checkbox v-show="item.value !== ''" :label="item.value" >{{item.label}}</el-checkbox>
                                    </template>
                                </el-checkbox-group>
                            </el-form-item>
                        </el-col>
                    </el-row>
                    <el-form-item label="选择城市">
                        <el-checkbox-group v-model="dialogForm.citys" @change="checkedCity">
                            <template v-for="item in selectProvince">
                                <el-checkbox :label="item.value">{{item.label}}</el-checkbox>
                            </template>
                        </el-checkbox-group>
                    </el-form-item>
                </el-form>
                <span slot="footer" class="dialog-footer">
                <el-button @click="dialogVisible = false">取 消</el-button>
                <el-button type="primary" @click="selectArea('dialogForm')">确 定</el-button>
                </span>
            </el-dialog>
            <!--选择地区弹窗结束-->
        </el-form>
    </div>
</template>
<script>
    export default{
        data(){
             return{
                 form:{
                     areaList:'',//所在地区的值
                     Region: [],
                     RegionCode: [],
                 },//输入表单
                 dialogForm:{
                     selectedArea:[],//弹窗选中的城市数组
                     provinces:[],
                     citys:[],
                 },//弹窗表单
                 selectProvince:[],//弹窗选中的省份
                 dialogVisible:false,//弹窗状态
                 provinceOptions: [
                     {
                         value: '',
                         label: '全国'
                     },
                     {
                         value: '33',
                         label: '安徽省',
                         children: [
                             {
                                 value: '3307',
                                 label: '安庆市'
                             },
                             {
                                 value: '3303',

                                 label: '蚌埠市'
                             },
                             {
                                 value: '3313',
                                 label: '巢湖市'
                             },
                             {
                                 value: '3311',
                                 label: '池州市'
                             },
                             {
                                 value: '3309',
                                 label: '滁州市'
                             },
                             {
                                 value: '3314',
                                 label: '阜阳市'
                             },
                             {
                                 value: '3301',
                                 label: '合肥市'
                             },
                             {
                                 value: '3305',
                                 label: '淮北市'
                             },
                             {
                                 value: '3312',
                                 label: '淮南市'
                             },
                             {
                                 value: '3308',
                                 label: '黄山市'
                             },
                             {
                                 value: '3315',
                                 label: '六安市'
                             },
                             {
                                 value: '3304',
                                 label: '马鞍山市'
                             },
                             {
                                 value: '3310',
                                 label: '宿州市'
                             },
                             {
                                 value: '3306',
                                 label: '铜陵市'
                             },
                             {
                                 value: '3302',
                                 label: '芜湖市'
                             },
                             {
                                 value: '3316',
                                 label: '宣城市'
                             },
                             {
                                 value: '3317',
                                 label: '亳州市'
                             }
                         ]
                     },
                     // {
                     //     value: '91',
                     //     label: '澳门',
                     // },
                     {
                         value: '10',
                         label: '北京市',
                     },
                     {
                         value: '34',
                         label: '福建省',
                         children: [
                             {
                                 value: '3401',
                                 label: '福州市'
                             },
                             {
                                 value: '3408',
                                 label: '龙岩市'
                             },
                             {
                                 value: '3407',
                                 label: '南平市'
                             },
                             {
                                 value: '3409',
                                 label: '宁德市'
                             },
                             {
                                 value: '3405',
                                 label: '莆田市'
                             },
                             {
                                 value: '3404',
                                 label: '泉州市'
                             },
                             {
                                 value: '3406',
                                 label: '三明市'
                             },
                             {
                                 value: '3402',
                                 label: '厦门市'
                             },
                             {
                                 value: '3403',
                                 label: '漳州市'
                             }
                         ]
                     },
                     {
                         value: '84',
                         label: '甘肃省',
                         children: [
                             {
                                 value: '8410',
                                 label: '白银市'
                             },
                             {
                                 value: '8411',
                                 label: '定西市'
                             },
                             {
                                 value: '8414',
                                 label: '甘南州'
                             },
                             {
                                 value: '8403',
                                 label: '嘉峪关市'
                             },
                             {
                                 value: '8405',
                                 label: '金昌市'
                             },
                             {
                                 value: '8406',
                                 label: '酒泉市'
                             },
                             {
                                 value: '8401',
                                 label: '兰州市'
                             },
                             {
                                 value: '8413',
                                 label: '临夏'
                             },
                             {
                                 value: '8412',
                                 label: '陇南市'
                             },
                             {
                                 value: '8409',
                                 label: '平凉市'
                             },
                             {
                                 value: '8408',
                                 label: '庆阳市'
                             },
                             {
                                 value: '8402',
                                 label: '天水市'
                             },
                             {
                                 value: '8404',
                                 label: '武威市'
                             },
                             {
                                 value: '8407',
                                 label: '张掖市'
                             }
                         ]
                     },
                     {
                         value: '40',
                         label: '广东省',
                         children: [
                             {
                                 value: '4019',
                                 label: '潮州市'
                             },
                             {
                                 value: '4010',
                                 label: '东莞市'
                             },
                             {
                                 value: '4013',
                                 label: '佛山市'
                             },
                             {
                                 value: '4001',
                                 label: '广州市'
                             },
                             {
                                 value: '4006',
                                 label: '河源市'
                             },
                             {
                                 value: '4008',
                                 label: '惠州市'
                             },
                             {
                                 value: '4012',
                                 label: '江门市'
                             },
                             {
                                 value: '4020',
                                 label: '揭阳市'
                             },
                             {
                                 value: '4016',
                                 label: '茂名市'
                             },
                             {
                                 value: '4007',
                                 label: '梅州市'
                             },
                             {
                                 value: '4018',
                                 label: '清远市'
                             },
                             {
                                 value: '4004',
                                 label: '汕头市'
                             },
                             {
                                 value: '4009',
                                 label: '汕尾市'
                             },
                             {
                                 value: '4005',
                                 label: '韶关市'
                             },
                             {
                                 value: '4002',
                                 label: '深圳市'
                             },
                             {
                                 value: '4014',
                                 label: '阳江市'
                             },
                             {
                                 value: '4021',
                                 label: '云浮市'
                             },
                             {
                                 value: '4015',
                                 label: '湛江市'
                             },
                             {
                                 value: '4017',
                                 label: '肇庆市'
                             },
                             {
                                 value: '4011',
                                 label: '中山市'
                             },
                             {
                                 value: '4003',
                                 label: '珠海市'
                             }
                         ]
                     },
                     {
                         value: '41',
                         label: '广西',
                         children: [
                             {
                                 value: '4110',
                                 label: '百色市'
                             },
                             {
                                 value: '4105',
                                 label: '北海市'
                             },
                             {
                                 value: '4114',
                                 label: '崇左市'
                             },
                             {
                                 value: '4106',
                                 label: '防城港市'
                             },
                             {
                                 value: '4108',
                                 label: '贵港市'
                             },
                             {
                                 value: '4103',
                                 label: '桂林市'
                             },
                             {
                                 value: '4112',
                                 label: '河池市'
                             },
                             {
                                 value: '4111',
                                 label: '贺州市'
                             },
                             {
                                 value: '4113',
                                 label: '来宾市'
                             },
                             {
                                 value: '4102',
                                 label: '柳州市'
                             },
                             {
                                 value: '4101',
                                 label: '南宁市'
                             },
                             {
                                 value: '4107',
                                 label: '钦州市'
                             },
                             {
                                 value: '4104',
                                 label: '梧州市'
                             },
                             {
                                 value: '4109',
                                 label: '玉林市'
                             }
                         ]
                     },
                     {
                         value: '63',
                         label: '贵州省',
                         children: [
                             {
                                 value: '6304',
                                 label: '安顺市'
                             },
                             {
                                 value: '6308',
                                 label: '毕节地区'
                             },
                             {
                                 value: '6301',
                                 label: '贵阳市'
                             },
                             {
                                 value: '6303',
                                 label: '六盘水市'
                             },
                             {
                                 value: '6309',
                                 label: '黔东南'
                             },
                             {
                                 value: '6306',
                                 label: '黔南'
                             },
                             {
                                 value: '6305',
                                 label: '黔西南'
                             },
                             {
                                 value: '6307',
                                 label: '铜仁地区'
                             },
                             {
                                 value: '6302',
                                 label: '遵义市'
                             }
                         ]
                     },
                     {
                         value: '93',
                         label: '国外',
                     },
                     {
                         value: '42',
                         label: '海南省',
                         children: [
                             {
                                 value: '4218',
                                 label: '白沙县'
                             },
                             {
                                 value: '4215',
                                 label: '保亭县'
                             },
                             {
                                 value: '4217',
                                 label: '昌江县'
                             },
                             {
                                 value: '4211',
                                 label: '澄迈县'
                             },
                             {
                                 value: '4209',
                                 label: '定安县'
                             },
                             {
                                 value: '4206',
                                 label: '东方市'
                             },
                             {
                                 value: '4201',
                                 label: '海口市'
                             },
                             {
                                 value: '4216',
                                 label: '乐东县'
                             },
                             {
                                 value: '4212',
                                 label: '临高县'
                             },
                             {
                                 value: '4213',
                                 label: '陵水县'
                             },
                             {
                                 value: '4203',
                                 label: '琼海市'
                             },
                             {
                                 value: '4214',
                                 label: '琼中县'
                             },
                             {
                                 value: '4202',
                                 label: '三亚市'
                             },
                             {
                                 value: '4210',
                                 label: '屯昌县'
                             },
                             {
                                 value: '4208',
                                 label: '万宁市'
                             },
                             {
                                 value: '4205',
                                 label: '文昌市'
                             },
                             {
                                 value: '4207',
                                 label: '五指山市'
                             },
                             {
                                 value: '4219',
                                 label: '洋浦'
                             },
                             {
                                 value: '4204',
                                 label: '儋州市'
                             }
                         ]
                     },
                     {
                         value: '12',
                         label: '河北省',
                         children: [
                             {
                                 value: '1207',
                                 label: '保定市'
                             },
                             {
                                 value: '1210',
                                 label: '沧州市'
                             },
                             {
                                 value: '1208',
                                 label: '承德市'
                             },
                             {
                                 value: '1211',
                                 label: '邯郸市'
                             },
                             {
                                 value: '1206',
                                 label: '衡水市'
                             },
                             {
                                 value: '1205',
                                 label: '廊坊市'
                             },
                             {
                                 value: '1202',
                                 label: '秦皇岛市'
                             },
                             {
                                 value: '1201',
                                 label: '石家庄市'
                             },
                             {
                                 value: '1203',
                                 label: '唐山市'
                             },
                             {
                                 value: '1209',
                                 label: '邢台市'
                             },
                             {
                                 value: '1204',
                                 label: '张家口市'
                             }
                         ]
                     },
                     {
                         value: '22',
                         label: '黑龙江省',
                         children: [
                             {
                                 value: '2206',
                                 label: '大庆市'
                             },
                             {
                                 value: '2213',
                                 label: '大兴安岭地区'
                             },
                             {
                                 value: '2201',
                                 label: '哈尔滨市'
                             },
                             {
                                 value: '2204',
                                 label: '鹤岗市'
                             },
                             {
                                 value: '2211',
                                 label: '黑河市'
                             },
                             {
                                 value: '2208',
                                 label: '佳木斯市'
                             },
                             {
                                 value: '2203',
                                 label: '鸡西市'
                             },
                             {
                                 value: '2210',
                                 label: '牡丹江市'
                             },
                             {
                                 value: '2202',
                                 label: '齐齐哈尔市'
                             },
                             {
                                 value: '2209',
                                 label: '七台河市'
                             },
                             {
                                 value: '2205',
                                 label: '双鸭山市'
                             },
                             {
                                 value: '2212',
                                 label: '绥化市'
                             },
                             {
                                 value: '2207',
                                 label: '伊春市'
                             }
                         ]
                     },
                     {
                         value: '70',
                         label: '河南省',
                         children: [
                             {
                                 value: '7004',
                                 label: '安阳市'
                             },
                             {
                                 value: '7008',
                                 label: '鹤壁市'
                             },
                             {
                                 value: '7007',
                                 label: '焦作市'
                             },
                             {
                                 value: '7018',
                                 label: '济源市'
                             },
                             {
                                 value: '7003',
                                 label: '开封市'
                             },
                             {
                                 value: '7002',
                                 label: '洛阳市'
                             },
                             {
                                 value: '7016',
                                 label: '南阳市'
                             },
                             {
                                 value: '7013',
                                 label: '平顶山市'
                             },
                             {
                                 value: '7009',
                                 label: '三门峡市'
                             },
                             {
                                 value: '7010',
                                 label: '商丘市'
                             },
                             {
                                 value: '7005',
                                 label: '新乡市'
                             },
                             {
                                 value: '7017',
                                 label: '信阳市'
                             },
                             {
                                 value: '7011',
                                 label: '许昌市'
                             },
                             {
                                 value: '7001',
                                 label: '郑州市'
                             },
                             {
                                 value: '7015',
                                 label: '周口市'
                             },
                             {
                                 value: '7014',
                                 label: '驻马店市'
                             },
                             {
                                 value: '7012',
                                 label: '漯河市'
                             },
                             {
                                 value: '7006',
                                 label: '濮阳市'
                             }
                         ]
                     },
                     {
                         value: '71',
                         label: '湖北省',
                         children: [
                             {
                                 value: '7113',
                                 label: '恩施'
                             },
                             {
                                 value: '7108',
                                 label: '鄂州市'
                             },
                             {
                                 value: '7110',
                                 label: '黄冈市'
                             },
                             {
                                 value: '7102',
                                 label: '黄石市'
                             },
                             {
                                 value: '7107',
                                 label: '荆门市'
                             },
                             {
                                 value: '7105',
                                 label: '荆州市'
                             },
                             {
                                 value: '7114',
                                 label: '潜江市'
                             },
                             {
                                 value: '7117',
                                 label: '神农架林区'
                             },
                             {
                                 value: '7104',
                                 label: '十堰市'
                             },
                             {
                                 value: '7112',
                                 label: '随州市'
                             },
                             {
                                 value: '7116',
                                 label: '天门市'
                             },
                             {
                                 value: '7101',
                                 label: '武汉市'
                             },
                             {
                                 value: '7103',
                                 label: '襄阳市'
                             },
                             {
                                 value: '7111',
                                 label: '咸宁市'
                             },
                             {
                                 value: '7115',
                                 label: '仙桃市'
                             },
                             {
                                 value: '7109',
                                 label: '孝感市'
                             },
                             {
                                 value: '7106',
                                 label: '宜昌市'
                             }
                         ]
                     },
                     {
                         value: '72',
                         label: '湖南省',
                         children: [
                             {
                                 value: '7206',
                                 label: '常德市'
                             },
                             {
                                 value: '7201',
                                 label: '长沙市'
                             },
                             {
                                 value: '7209',
                                 label: '郴州市'
                             },
                             {
                                 value: '7204',
                                 label: '衡阳市'
                             },
                             {
                                 value: '7212',
                                 label: '怀化市'
                             },
                             {
                                 value: '7210',
                                 label: '娄底市'
                             },
                             {
                                 value: '7208',
                                 label: '邵阳市'
                             },
                             {
                                 value: '7203',
                                 label: '湘潭市'
                             },
                             {
                                 value: '7214',
                                 label: '湘西'
                             },
                             {
                                 value: '7205',
                                 label: '益阳市'
                             },
                             {
                                 value: '7211',
                                 label: '永州市'
                             },
                             {
                                 value: '7207',
                                 label: '岳阳市'
                             },
                             {
                                 value: '7213',
                                 label: '张家界市'
                             },
                             {
                                 value: '7202',
                                 label: '株洲市'
                             }
                         ]
                     },
                     {
                         value: '31',
                         label: '江苏省',
                         children: [
                             {
                                 value: '3107',
                                 label: '常州市'
                             },
                             {
                                 value: '3111',
                                 label: '淮安市'
                             },
                             {
                                 value: '3109',
                                 label: '连云港市'
                             },
                             {
                                 value: '3101',
                                 label: '南京市'
                             },
                             {
                                 value: '3106',
                                 label: '南通市'
                             },
                             {
                                 value: '3113',
                                 label: '宿迁市'
                             },
                             {
                                 value: '3102',
                                 label: '苏州市'
                             },
                             {
                                 value: '3112',
                                 label: '泰州市'
                             },
                             {
                                 value: '3103',
                                 label: '无锡市'
                             },
                             {
                                 value: '3108',
                                 label: '徐州市'
                             },
                             {
                                 value: '3110',
                                 label: '盐城市'
                             },
                             {
                                 value: '3105',
                                 label: '扬州市'
                             },
                             {
                                 value: '3104',
                                 label: '镇江市'
                             }
                         ]
                     },
                     {
                         value: '36',
                         label: '江西省',
                         children: [
                             {
                                 value: '3610',
                                 label: '抚州市'
                             },
                             {
                                 value: '3607',
                                 label: '赣州市'
                             },
                             {
                                 value: '3608',
                                 label: '吉安市'
                             },
                             {
                                 value: '3602',
                                 label: '景德镇市'
                             },
                             {
                                 value: '3604',
                                 label: '九江市'
                             },
                             {
                                 value: '3601',
                                 label: '南昌市'
                             },
                             {
                                 value: '3603',
                                 label: '萍乡市'
                             },
                             {
                                 value: '3611',
                                 label: '上饶市'
                             },
                             {
                                 value: '3605',
                                 label: '新余市'
                             },
                             {
                                 value: '3609',
                                 label: '宜春市'
                             },
                             {
                                 value: '3606',
                                 label: '鹰潭市'
                             }
                         ]
                     },
                     {
                         value: '21',
                         label: '吉林省',
                         children: [
                             {
                                 value: '2108',
                                 label: '白城市'
                             },
                             {
                                 value: '2106',
                                 label: '白山市'
                             },
                             {
                                 value: '2101',
                                 label: '长春市'
                             },
                             {
                                 value: '2102',
                                 label: '吉林市'
                             },
                             {
                                 value: '2104',
                                 label: '辽源市'
                             },
                             {
                                 value: '2103',
                                 label: '四平市'
                             },
                             {
                                 value: '2107',
                                 label: '松原市'
                             },
                             {
                                 value: '2105',
                                 label: '通化市'
                             },
                             {
                                 value: '2109',
                                 label: '延边州'
                             }
                         ]
                     },
                     {
                         value: '20',
                         label: '辽宁省',
                         children: [
                             {
                                 value: '2003',
                                 label: '鞍山市'
                             },
                             {
                                 value: '2012',
                                 label: '本溪市'
                             },
                             {
                                 value: '2013',
                                 label: '朝阳市'
                             },
                             {
                                 value: '2002',
                                 label: '大连市'
                             },
                             {
                                 value: '2005',
                                 label: '丹东市'
                             },
                             {
                                 value: '2008',
                                 label: '抚顺市'
                             },
                             {
                                 value: '2011',
                                 label: '阜新市'
                             },
                             {
                                 value: '2014',
                                 label: '葫芦岛市'
                             },
                             {
                                 value: '2004',
                                 label: '锦州市'
                             },
                             {
                                 value: '2010',
                                 label: '辽阳市'
                             },
                             {
                                 value: '2006',
                                 label: '盘锦市'
                             },
                             {
                                 value: '2001',
                                 label: '沈阳市'
                             },
                             {
                                 value: '2007',
                                 label: '铁岭市'
                             },
                             {
                                 value: '2009',
                                 label: '营口市'
                             }
                         ]
                     },
                     {
                         value: '13',
                         label: '内蒙古',
                         children: [
                             {
                                 value: '1312',
                                 label: '阿拉善盟'
                             },
                             {
                                 value: '1302',
                                 label: '包头市'
                             },
                             {
                                 value: '1310',
                                 label: '巴彦淖尔市'
                             },
                             {
                                 value: '1306',
                                 label: '赤峰市'
                             },
                             {
                                 value: '1309',
                                 label: '鄂尔多斯市'
                             },
                             {
                                 value: '1314',
                                 label: '二连浩特'
                             },
                             {
                                 value: '1301',
                                 label: '呼和浩特市'
                             },
                             {
                                 value: '1303',
                                 label: '呼伦贝尔市'
                             },
                             {
                                 value: '1313',
                                 label: '满洲里'
                             },
                             {
                                 value: '1305',
                                 label: '通辽市'
                             },
                             {
                                 value: '1311',
                                 label: '乌海市'
                             },
                             {
                                 value: '1308',
                                 label: '乌兰察布市'
                             },
                             {
                                 value: '1307',
                                 label: '锡林郭勒盟'
                             },
                             {
                                 value: '1304',
                                 label: '兴安盟'
                             }
                         ]
                     },
                     {
                         value: '82',
                         label: '宁夏',
                         children: [
                             {
                                 value: '8204',
                                 label: '固原市'
                             },
                             {
                                 value: '8202',
                                 label: '石嘴山市'
                             },
                             {
                                 value: '8203',
                                 label: '吴忠市'
                             },
                             {
                                 value: '8201',
                                 label: '银川市'
                             },
                             {
                                 value: '8205',
                                 label: '中卫市'
                             }
                         ]
                     },
                     {
                         value: '81',
                         label: '青海省',
                         children: [
                             {
                                 value: '8107',
                                 label: '果洛州'
                             },
                             {
                                 value: '8104',
                                 label: '海北州'
                             },
                             {
                                 value: '8102',
                                 label: '海东地区'
                             },
                             {
                                 value: '8103',
                                 label: '海南州'
                             },
                             {
                                 value: '8105',
                                 label: '海西蒙古族州'
                             },
                             {
                                 value: '8106',
                                 label: '黄南州'
                             },
                             {
                                 value: '8101',
                                 label: '西宁市'
                             },
                             {
                                 value: '8108',
                                 label: '玉树州'
                             }
                         ]
                     },
                     {
                         value: '32',
                         label: '山东省',
                         children: [
                             {
                                 value: '3213',
                                 label: '滨州市'
                             },
                             {
                                 value: '3209',
                                 label: '德州市'
                             },
                             {
                                 value: '3214',
                                 label: '东营市'
                             },
                             {
                                 value: '3216',
                                 label: '菏泽市'
                             },
                             {
                                 value: '3201',
                                 label: '济南市'
                             },
                             {
                                 value: '3207',
                                 label: '济宁市'
                             },
                             {
                                 value: '3212',
                                 label: '莱芜市'
                             },
                             {
                                 value: '3215',
                                 label: '聊城市'
                             },
                             {
                                 value: '3217',
                                 label: '临沂市'
                             },
                             {
                                 value: '3202',
                                 label: '青岛市'
                             },
                             {
                                 value: '3211',
                                 label: '日照市'
                             },
                             {
                                 value: '3205',
                                 label: '泰安市'
                             },
                             {
                                 value: '3206',
                                 label: '潍坊市'
                             },
                             {
                                 value: '3210',
                                 label: '威海市'
                             },
                             {
                                 value: '3203',
                                 label: '烟台市'
                             },
                             {
                                 value: '3208',
                                 label: '枣庄市'
                             },
                             {
                                 value: '3204',
                                 label: '淄博市'
                             }
                         ]
                     },
                     {
                         value: '30',
                         label: '上海市',
                     },
                     {
                         value: '80',
                         label: '陕西省',
                         children: [
                             {
                                 value: '8009',
                                 label: '安康市'
                             },
                             {
                                 value: '8002',
                                 label: '宝鸡市'
                             },
                             {
                                 value: '8008',
                                 label: '汉中市'
                             },
                             {
                                 value: '8010',
                                 label: '商洛市'
                             },
                             {
                                 value: '8007',
                                 label: '铜川市'
                             },
                             {
                                 value: '8004',
                                 label: '渭南市'
                             },
                             {
                                 value: '8001',
                                 label: '西安市'
                             },
                             {
                                 value: '8003',
                                 label: '咸阳市'
                             },
                             {
                                 value: '8005',
                                 label: '延安市'
                             },
                             {
                                 value: '8011',
                                 label: '杨凌'
                             },
                             {
                                 value: '8006',
                                 label: '榆林市'
                             }
                         ]
                     },
                     {
                         value: '14',
                         label: '山西省',
                         children: [
                             {
                                 value: '1404',
                                 label: '长治市'
                             },
                             {
                                 value: '1402',
                                 label: '大同市'
                             },
                             {
                                 value: '1405',
                                 label: '晋城市'
                             },
                             {
                                 value: '1408',
                                 label: '晋中市'
                             },
                             {
                                 value: '1409',
                                 label: '临汾市'
                             },
                             {
                                 value: '1410',
                                 label: '吕梁市'
                             },
                             {
                                 value: '1406',
                                 label: '朔州市'
                             },
                             {
                                 value: '1401',
                                 label: '太原市'
                             },
                             {
                                 value: '1407',
                                 label: '忻州市'
                             },
                             {
                                 value: '1403',
                                 label: '阳泉市'
                             },
                             {
                                 value: '1411',
                                 label: '运城市'
                             }
                         ]
                     },
                     {
                         value: '61',
                         label: '四川省',
                         children: [
                             {
                                 value: '6118',
                                 label: '阿坝州'
                             },
                             {
                                 value: '6114',
                                 label: '巴中市'
                             },
                             {
                                 value: '6101',
                                 label: '成都市'
                             },
                             {
                                 value: '6113',
                                 label: '达州市'
                             },
                             {
                                 value: '6102',
                                 label: '德阳市'
                             },
                             {
                                 value: '6120',
                                 label: '甘孜州'
                             },
                             {
                                 value: '6116',
                                 label: '广安市'
                             },
                             {
                                 value: '6115',
                                 label: '广元市'
                             },
                             {
                                 value: '6110',
                                 label: '乐山市'
                             },
                             {
                                 value: '6121',
                                 label: '凉山州'
                             },
                             {
                                 value: '6104',
                                 label: '眉山市'
                             },
                             {
                                 value: '6103',
                                 label: '绵阳市'
                             },
                             {
                                 value: '6106',
                                 label: '南充市'
                             },
                             {
                                 value: '6108',
                                 label: '内江市'
                             },
                             {
                                 value: '6119',
                                 label: '攀枝花市'
                             },
                             {
                                 value: '6112',
                                 label: '遂宁市'
                             },
                             {
                                 value: '6111',
                                 label: '雅安市'
                             },
                             {
                                 value: '6109',
                                 label: '宜宾市'
                             },
                             {
                                 value: '6107',
                                 label: '自贡市'
                             },
                             {
                                 value: '6117',
                                 label: '资阳市'
                             },
                             {
                                 value: '6105',
                                 label: '泸州市'
                             }
                         ]
                     },
                     // {
                     //     value: '92',
                     //     label: '台湾',
                     // },
                     {
                         value: '11',
                         label: '天津市',
                     },
                     // {
                     //     value: '90',
                     //     label: '香港',
                     // },
                     {
                         value: '64',
                         label: '西藏',
                         children: [
                             {
                                 value: '6407',
                                 label: '阿里地区'
                             },
                             {
                                 value: '6405',
                                 label: '昌都地区'
                             },
                             {
                                 value: '6401',
                                 label: '拉萨市'
                             },
                             {
                                 value: '6404',
                                 label: '林芝地区'
                             },
                             {
                                 value: '6406',
                                 label: '那曲地区'
                             },
                             {
                                 value: '6402',
                                 label: '日喀则地区'
                             },
                             {
                                 value: '6403',
                                 label: '山南地区'
                             }
                         ]
                     },
                     {
                         value: '83',
                         label: '新疆',
                         children: [
                             {
                                 value: '8311',
                                 label: '阿克苏地区'
                             },
                             {
                                 value: '8317',
                                 label: '阿拉尔市'
                             },
                             {
                                 value: '8303',
                                 label: '阿勒泰地区'
                             },
                             {
                                 value: '8308',
                                 label: '巴音郭楞'
                             },
                             {
                                 value: '8305',
                                 label: '博尔塔拉'
                             },
                             {
                                 value: '8306',
                                 label: '昌吉'
                             },
                             {
                                 value: '8309',
                                 label: '哈密地区'
                             },
                             {
                                 value: '8310',
                                 label: '和田地区'
                             },
                             {
                                 value: '8313',
                                 label: '喀什地区'
                             },
                             {
                                 value: '8314',
                                 label: '克拉玛依市'
                             },
                             {
                                 value: '8312',
                                 label: '克孜勒苏'
                             },
                             {
                                 value: '8315',
                                 label: '石河子市'
                             },
                             {
                                 value: '8304',
                                 label: '塔城地区'
                             },
                             {
                                 value: '8307',
                                 label: '吐鲁番地区'
                             },
                             {
                                 value: '8318',
                                 label: '图木舒克市'
                             },
                             {
                                 value: '8316',
                                 label: '五家渠市'
                             },
                             {
                                 value: '8301',
                                 label: '乌鲁木齐市'
                             },
                             {
                                 value: '8302',
                                 label: '伊犁州'
                             }
                         ]
                     },
                     {
                         value: '62',
                         label: '云南省',
                         children: [
                             {
                                 value: '6213',
                                 label: '保山市'
                             },
                             {
                                 value: '6205',
                                 label: '楚雄州'
                             },
                             {
                                 value: '6212',
                                 label: '大理'
                             },
                             {
                                 value: '6214',
                                 label: '德宏'
                             },
                             {
                                 value: '6208',
                                 label: '迪庆州'
                             },
                             {
                                 value: '6206',
                                 label: '红河哈尼族州'
                             },
                             {
                                 value: '6201',
                                 label: '昆明市'
                             },
                             {
                                 value: '6207',
                                 label: '丽江市'
                             },
                             {
                                 value: '6216',
                                 label: '临沧市'
                             },
                             {
                                 value: '6215',
                                 label: '怒江'
                             },
                             {
                                 value: '6211',
                                 label: '普洱市'
                             },
                             {
                                 value: '6202',
                                 label: '曲靖市'
                             },
                             {
                                 value: '6209',
                                 label: '文山州'
                             },
                             {
                                 value: '6210',
                                 label: '西双版纳州'
                             },
                             {
                                 value: '6203',
                                 label: '玉溪市'
                             },
                             {
                                 value: '6204',
                                 label: '昭通市'
                             }
                         ]
                     },
                     {
                         value: '35',
                         label: '浙江省',
                         children: [
                             {
                                 value: '3501',
                                 label: '杭州市'
                             },
                             {
                                 value: '3505',
                                 label: '湖州市'
                             },
                             {
                                 value: '3504',
                                 label: '嘉兴市'
                             },
                             {
                                 value: '3507',
                                 label: '金华市'
                             },
                             {
                                 value: '3511',
                                 label: '丽水市'
                             },
                             {
                                 value: '3502',
                                 label: '宁波市'
                             },
                             {
                                 value: '3506',
                                 label: '绍兴市'
                             },
                             {
                                 value: '3510',
                                 label: '台州市'
                             },
                             {
                                 value: '3503',
                                 label: '温州市'
                             },
                             {
                                 value: '3509',
                                 label: '舟山市'
                             },
                             {
                                 value: '3508',
                                 label: '衢州市'
                             }
                         ]
                     },
                     {
                         value: '60',
                         label: '重庆市',
                     }
                 ],//省市数据
                 cityOptions:[
                     {
                         "label": "北京市",
                         "value": "10"
                     },
                     {
                         "label": "天津市",
                         "value": "11"
                     },
                     {
                         "label": "石家庄市",
                         "value": "1201"
                     },
                     {
                         "label": "秦皇岛市",
                         "value": "1202"
                     },
                     {
                         "label": "唐山市",
                         "value": "1203"
                     },
                     {
                         "label": "张家口市",
                         "value": "1204"
                     },
                     {
                         "label": "廊坊市",
                         "value": "1205"
                     },
                     {
                         "label": "衡水市",
                         "value": "1206"
                     },
                     {
                         "label": "保定市",
                         "value": "1207"
                     },
                     {
                         "label": "承德市",
                         "value": "1208"
                     },
                     {
                         "label": "邢台市",
                         "value": "1209"
                     },
                     {
                         "label": "沧州市",
                         "value": "1210"
                     },
                     {
                         "label": "邯郸市",
                         "value": "1211"
                     },
                     {
                         "label": "呼和浩特市",
                         "value": "1301"
                     },
                     {
                         "label": "包头市",
                         "value": "1302"
                     },
                     {
                         "label": "呼伦贝尔市",
                         "value": "1303"
                     },
                     {
                         "label": "兴安盟",
                         "value": "1304"
                     },
                     {
                         "label": "通辽市",
                         "value": "1305"
                     },
                     {
                         "label": "赤峰市",
                         "value": "1306"
                     },
                     {
                         "label": "锡林郭勒盟",
                         "value": "1307"
                     },
                     {
                         "label": "乌兰察布市",
                         "value": "1308"
                     },
                     {
                         "label": "鄂尔多斯市",
                         "value": "1309"
                     },
                     {
                         "label": "巴彦淖尔市",
                         "value": "1310"
                     },
                     {
                         "label": "乌海市",
                         "value": "1311"
                     },
                     {
                         "label": "阿拉善盟",
                         "value": "1312"
                     },
                     {
                         "label": "满洲里",
                         "value": "1313"
                     },
                     {
                         "label": "二连浩特",
                         "value": "1314"
                     },
                     {
                         "label": "太原市",
                         "value": "1401"
                     },
                     {
                         "label": "大同市",
                         "value": "1402"
                     },
                     {
                         "label": "阳泉市",
                         "value": "1403"
                     },
                     {
                         "label": "长治市",
                         "value": "1404"
                     },
                     {
                         "label": "晋城市",
                         "value": "1405"
                     },
                     {
                         "label": "朔州市",
                         "value": "1406"
                     },
                     {
                         "label": "忻州市",
                         "value": "1407"
                     },
                     {
                         "label": "晋中市",
                         "value": "1408"
                     },
                     {
                         "label": "临汾市",
                         "value": "1409"
                     },
                     {
                         "label": "吕梁市",
                         "value": "1410"
                     },
                     {
                         "label": "运城市",
                         "value": "1411"
                     },
                     {
                         "label": "沈阳市",
                         "value": "2001"
                     },
                     {
                         "label": "大连市",
                         "value": "2002"
                     },
                     {
                         "label": "鞍山市",
                         "value": "2003"
                     },
                     {
                         "label": "锦州市",
                         "value": "2004"
                     },
                     {
                         "label": "丹东市",
                         "value": "2005"
                     },
                     {
                         "label": "盘锦市",
                         "value": "2006"
                     },
                     {
                         "label": "铁岭市",
                         "value": "2007"
                     },
                     {
                         "label": "抚顺市",
                         "value": "2008"
                     },
                     {
                         "label": "营口市",
                         "value": "2009"
                     },
                     {
                         "label": "辽阳市",
                         "value": "2010"
                     },
                     {
                         "label": "阜新市",
                         "value": "2011"
                     },
                     {
                         "label": "本溪市",
                         "value": "2012"
                     },
                     {
                         "label": "朝阳市",
                         "value": "2013"
                     },
                     {
                         "label": "葫芦岛市",
                         "value": "2014"
                     },
                     {
                         "label": "长春市",
                         "value": "2101"
                     },
                     {
                         "label": "吉林市",
                         "value": "2102"
                     },
                     {
                         "label": "四平市",
                         "value": "2103"
                     },
                     {
                         "label": "辽源市",
                         "value": "2104"
                     },
                     {
                         "label": "通化市",
                         "value": "2105"
                     },
                     {
                         "label": "白山市",
                         "value": "2106"
                     },
                     {
                         "label": "松原市",
                         "value": "2107"
                     },
                     {
                         "label": "白城市",
                         "value": "2108"
                     },
                     {
                         "label": "延边州",
                         "value": "2109"
                     },
                     {
                         "label": "哈尔滨市",
                         "value": "2201"
                     },
                     {
                         "label": "齐齐哈尔市",
                         "value": "2202"
                     },
                     {
                         "label": "鸡西市",
                         "value": "2203"
                     },
                     {
                         "label": "鹤岗市",
                         "value": "2204"
                     },
                     {
                         "label": "双鸭山市",
                         "value": "2205"
                     },
                     {
                         "label": "大庆市",
                         "value": "2206"
                     },
                     {
                         "label": "伊春市",
                         "value": "2207"
                     },
                     {
                         "label": "佳木斯市",
                         "value": "2208"
                     },
                     {
                         "label": "七台河市",
                         "value": "2209"
                     },
                     {
                         "label": "牡丹江市",
                         "value": "2210"
                     },
                     {
                         "label": "黑河市",
                         "value": "2211"
                     },
                     {
                         "label": "绥化市",
                         "value": "2212"
                     },
                     {
                         "label": "大兴安岭地区",
                         "value": "2213"
                     },
                     {
                         "label": "闸北区",
                         "value": "3015"
                     },
                     {
                         "label": "上海市",
                         "value": "30"
                     },
                     {
                         "label": "南京市",
                         "value": "3101"
                     },
                     {
                         "label": "苏州市",
                         "value": "3102"
                     },
                     {
                         "label": "无锡市",
                         "value": "3103"
                     },
                     {
                         "label": "镇江市",
                         "value": "3104"
                     },
                     {
                         "label": "扬州市",
                         "value": "3105"
                     },
                     {
                         "label": "南通市",
                         "value": "3106"
                     },
                     {
                         "label": "常州市",
                         "value": "3107"
                     },
                     {
                         "label": "徐州市",
                         "value": "3108"
                     },
                     {
                         "label": "连云港市",
                         "value": "3109"
                     },
                     {
                         "label": "盐城市",
                         "value": "3110"
                     },
                     {
                         "label": "淮安市",
                         "value": "3111"
                     },
                     {
                         "label": "泰州市",
                         "value": "3112"
                     },
                     {
                         "label": "宿迁市",
                         "value": "3113"
                     },
                     {
                         "label": "济南市",
                         "value": "3201"
                     },
                     {
                         "label": "青岛市",
                         "value": "3202"
                     },
                     {
                         "label": "烟台市",
                         "value": "3203"
                     },
                     {
                         "label": "淄博市",
                         "value": "3204"
                     },
                     {
                         "label": "泰安市",
                         "value": "3205"
                     },
                     {
                         "label": "潍坊市",
                         "value": "3206"
                     },
                     {
                         "label": "济宁市",
                         "value": "3207"
                     },
                     {
                         "label": "枣庄市",
                         "value": "3208"
                     },
                     {
                         "label": "德州市",
                         "value": "3209"
                     },
                     {
                         "label": "威海市",
                         "value": "3210"
                     },
                     {
                         "label": "日照市",
                         "value": "3211"
                     },
                     {
                         "label": "莱芜市",
                         "value": "3212"
                     },
                     {
                         "label": "滨州市",
                         "value": "3213"
                     },
                     {
                         "label": "东营市",
                         "value": "3214"
                     },
                     {
                         "label": "聊城市",
                         "value": "3215"
                     },
                     {
                         "label": "菏泽市",
                         "value": "3216"
                     },
                     {
                         "label": "临沂市",
                         "value": "3217"
                     },
                     {
                         "label": "合肥市",
                         "value": "3301"
                     },
                     {
                         "label": "芜湖市",
                         "value": "3302"
                     },
                     {
                         "label": "蚌埠市",
                         "value": "3303"
                     },
                     {
                         "label": "马鞍山市",
                         "value": "3304"
                     },
                     {
                         "label": "淮北市",
                         "value": "3305"
                     },
                     {
                         "label": "铜陵市",
                         "value": "3306"
                     },
                     {
                         "label": "安庆市",
                         "value": "3307"
                     },
                     {
                         "label": "黄山市",
                         "value": "3308"
                     },
                     {
                         "label": "滁州市",
                         "value": "3309"
                     },
                     {
                         "label": "宿州市",
                         "value": "3310"
                     },
                     {
                         "label": "池州市",
                         "value": "3311"
                     },
                     {
                         "label": "淮南市",
                         "value": "3312"
                     },
                     {
                         "label": "巢湖市",
                         "value": "3313"
                     },
                     {
                         "label": "阜阳市",
                         "value": "3314"
                     },
                     {
                         "label": "六安市",
                         "value": "3315"
                     },
                     {
                         "label": "宣城市",
                         "value": "3316"
                     },
                     {
                         "label": "亳州市",
                         "value": "3317"
                     },
                     {
                         "label": "福州市",
                         "value": "3401"
                     },
                     {
                         "label": "厦门市",
                         "value": "3402"
                     },
                     {
                         "label": "漳州市",
                         "value": "3403"
                     },
                     {
                         "label": "泉州市",
                         "value": "3404"
                     },
                     {
                         "label": "莆田市",
                         "value": "3405"
                     },
                     {
                         "label": "三明市",
                         "value": "3406"
                     },
                     {
                         "label": "南平市",
                         "value": "3407"
                     },
                     {
                         "label": "龙岩市",
                         "value": "3408"
                     },
                     {
                         "label": "宁德市",
                         "value": "3409"
                     },
                     {
                         "label": "杭州市",
                         "value": "3501"
                     },
                     {
                         "label": "宁波市",
                         "value": "3502"
                     },
                     {
                         "label": "温州市",
                         "value": "3503"
                     },
                     {
                         "label": "嘉兴市",
                         "value": "3504"
                     },
                     {
                         "label": "湖州市",
                         "value": "3505"
                     },
                     {
                         "label": "绍兴市",
                         "value": "3506"
                     },
                     {
                         "label": "金华市",
                         "value": "3507"
                     },
                     {
                         "label": "衢州市",
                         "value": "3508"
                     },
                     {
                         "label": "舟山市",
                         "value": "3509"
                     },
                     {
                         "label": "台州市",
                         "value": "3510"
                     },
                     {
                         "label": "丽水市",
                         "value": "3511"
                     },
                     {
                         "label": "南昌市",
                         "value": "3601"
                     },
                     {
                         "label": "景德镇市",
                         "value": "3602"
                     },
                     {
                         "label": "萍乡市",
                         "value": "3603"
                     },
                     {
                         "label": "九江市",
                         "value": "3604"
                     },
                     {
                         "label": "新余市",
                         "value": "3605"
                     },
                     {
                         "label": "鹰潭市",
                         "value": "3606"
                     },
                     {
                         "label": "赣州市",
                         "value": "3607"
                     },
                     {
                         "label": "吉安市",
                         "value": "3608"
                     },
                     {
                         "label": "宜春市",
                         "value": "3609"
                     },
                     {
                         "label": "抚州市",
                         "value": "3610"
                     },
                     {
                         "label": "上饶市",
                         "value": "3611"
                     },
                     {
                         "label": "广州市",
                         "value": "4001"
                     },
                     {
                         "label": "深圳市",
                         "value": "4002"
                     },
                     {
                         "label": "珠海市",
                         "value": "4003"
                     },
                     {
                         "label": "汕头市",
                         "value": "4004"
                     },
                     {
                         "label": "韶关市",
                         "value": "4005"
                     },
                     {
                         "label": "河源市",
                         "value": "4006"
                     },
                     {
                         "label": "梅州市",
                         "value": "4007"
                     },
                     {
                         "label": "惠州市",
                         "value": "4008"
                     },
                     {
                         "label": "汕尾市",
                         "value": "4009"
                     },
                     {
                         "label": "东莞市",
                         "value": "4010"
                     },
                     {
                         "label": "中山市",
                         "value": "4011"
                     },
                     {
                         "label": "江门市",
                         "value": "4012"
                     },
                     {
                         "label": "佛山市",
                         "value": "4013"
                     },
                     {
                         "label": "阳江市",
                         "value": "4014"
                     },
                     {
                         "label": "湛江市",
                         "value": "4015"
                     },
                     {
                         "label": "茂名市",
                         "value": "4016"
                     },
                     {
                         "label": "肇庆市",
                         "value": "4017"
                     },
                     {
                         "label": "清远市",
                         "value": "4018"
                     },
                     {
                         "label": "潮州市",
                         "value": "4019"
                     },
                     {
                         "label": "揭阳市",
                         "value": "4020"
                     },
                     {
                         "label": "云浮市",
                         "value": "4021"
                     },
                     {
                         "label": "南宁市",
                         "value": "4101"
                     },
                     {
                         "label": "柳州市",
                         "value": "4102"
                     },
                     {
                         "label": "桂林市",
                         "value": "4103"
                     },
                     {
                         "label": "梧州市",
                         "value": "4104"
                     },
                     {
                         "label": "北海市",
                         "value": "4105"
                     },
                     {
                         "label": "防城港市",
                         "value": "4106"
                     },
                     {
                         "label": "钦州市",
                         "value": "4107"
                     },
                     {
                         "label": "贵港市",
                         "value": "4108"
                     },
                     {
                         "label": "玉林市",
                         "value": "4109"
                     },
                     {
                         "label": "百色市",
                         "value": "4110"
                     },
                     {
                         "label": "贺州市",
                         "value": "4111"
                     },
                     {
                         "label": "河池市",
                         "value": "4112"
                     },
                     {
                         "label": "来宾市",
                         "value": "4113"
                     },
                     {
                         "label": "崇左市",
                         "value": "4114"
                     },
                     {
                         "label": "海口市",
                         "value": "4201"
                     },
                     {
                         "label": "三亚市",
                         "value": "4202"
                     },
                     {
                         "label": "琼海市",
                         "value": "4203"
                     },
                     {
                         "label": "儋州市",
                         "value": "4204"
                     },
                     {
                         "label": "文昌市",
                         "value": "4205"
                     },
                     {
                         "label": "东方市",
                         "value": "4206"
                     },
                     {
                         "label": "五指山市",
                         "value": "4207"
                     },
                     {
                         "label": "万宁市",
                         "value": "4208"
                     },
                     {
                         "label": "定安县",
                         "value": "4209"
                     },
                     {
                         "label": "屯昌县",
                         "value": "4210"
                     },
                     {
                         "label": "澄迈县",
                         "value": "4211"
                     },
                     {
                         "label": "临高县",
                         "value": "4212"
                     },
                     {
                         "label": "陵水县",
                         "value": "4213"
                     },
                     {
                         "label": "琼中县",
                         "value": "4214"
                     },
                     {
                         "label": "保亭县",
                         "value": "4215"
                     },
                     {
                         "label": "乐东县",
                         "value": "4216"
                     },
                     {
                         "label": "昌江县",
                         "value": "4217"
                     },
                     {
                         "label": "白沙县",
                         "value": "4218"
                     },
                     {
                         "label": "洋浦",
                         "value": "4219"
                     },
                     {
                         "label": "重庆市",
                         "value": "60"
                     },
                     {
                         "label": "成都市",
                         "value": "6101"
                     },
                     {
                         "label": "德阳市",
                         "value": "6102"
                     },
                     {
                         "label": "绵阳市",
                         "value": "6103"
                     },
                     {
                         "label": "眉山市",
                         "value": "6104"
                     },
                     {
                         "label": "泸州市",
                         "value": "6105"
                     },
                     {
                         "label": "南充市",
                         "value": "6106"
                     },
                     {
                         "label": "自贡市",
                         "value": "6107"
                     },
                     {
                         "label": "内江市",
                         "value": "6108"
                     },
                     {
                         "label": "宜宾市",
                         "value": "6109"
                     },
                     {
                         "label": "乐山市",
                         "value": "6110"
                     },
                     {
                         "label": "雅安市",
                         "value": "6111"
                     },
                     {
                         "label": "遂宁市",
                         "value": "6112"
                     },
                     {
                         "label": "达州市",
                         "value": "6113"
                     },
                     {
                         "label": "巴中市",
                         "value": "6114"
                     },
                     {
                         "label": "广元市",
                         "value": "6115"
                     },
                     {
                         "label": "广安市",
                         "value": "6116"
                     },
                     {
                         "label": "资阳市",
                         "value": "6117"
                     },
                     {
                         "label": "阿坝州",
                         "value": "6118"
                     },
                     {
                         "label": "攀枝花市",
                         "value": "6119"
                     },
                     {
                         "label": "甘孜州",
                         "value": "6120"
                     },
                     {
                         "label": "凉山州",
                         "value": "6121"
                     },
                     {
                         "label": "昆明市",
                         "value": "6201"
                     },
                     {
                         "label": "曲靖市",
                         "value": "6202"
                     },
                     {
                         "label": "玉溪市",
                         "value": "6203"
                     },
                     {
                         "label": "昭通市",
                         "value": "6204"
                     },
                     {
                         "label": "楚雄州",
                         "value": "6205"
                     },
                     {
                         "label": "红河哈尼族州",
                         "value": "6206"
                     },
                     {
                         "label": "丽江市",
                         "value": "6207"
                     },
                     {
                         "label": "迪庆州",
                         "value": "6208"
                     },
                     {
                         "label": "文山州",
                         "value": "6209"
                     },
                     {
                         "label": "西双版纳州",
                         "value": "6210"
                     },
                     {
                         "label": "普洱市",
                         "value": "6211"
                     },
                     {
                         "label": "大理",
                         "value": "6212"
                     },
                     {
                         "label": "保山市",
                         "value": "6213"
                     },
                     {
                         "label": "德宏",
                         "value": "6214"
                     },
                     {
                         "label": "怒江",
                         "value": "6215"
                     },
                     {
                         "label": "临沧市",
                         "value": "6216"
                     },
                     {
                         "label": "贵阳市",
                         "value": "6301"
                     },
                     {
                         "label": "遵义市",
                         "value": "6302"
                     },
                     {
                         "label": "六盘水市",
                         "value": "6303"
                     },
                     {
                         "label": "安顺市",
                         "value": "6304"
                     },
                     {
                         "label": "黔西南",
                         "value": "6305"
                     },
                     {
                         "label": "黔南",
                         "value": "6306"
                     },
                     {
                         "label": "铜仁地区",
                         "value": "6307"
                     },
                     {
                         "label": "毕节地区",
                         "value": "6308"
                     },
                     {
                         "label": "黔东南",
                         "value": "6309"
                     },
                     {
                         "label": "拉萨市",
                         "value": "6401"
                     },
                     {
                         "label": "日喀则地区",
                         "value": "6402"
                     },
                     {
                         "label": "山南地区",
                         "value": "6403"
                     },
                     {
                         "label": "林芝地区",
                         "value": "6404"
                     },
                     {
                         "label": "昌都地区",
                         "value": "6405"
                     },
                     {
                         "label": "那曲地区",
                         "value": "6406"
                     },
                     {
                         "label": "阿里地区",
                         "value": "6407"
                     },
                     {
                         "label": "郑州市",
                         "value": "7001"
                     },
                     {
                         "label": "洛阳市",
                         "value": "7002"
                     },
                     {
                         "label": "开封市",
                         "value": "7003"
                     },
                     {
                         "label": "安阳市",
                         "value": "7004"
                     },
                     {
                         "label": "新乡市",
                         "value": "7005"
                     },
                     {
                         "label": "濮阳市",
                         "value": "7006"
                     },
                     {
                         "label": "焦作市",
                         "value": "7007"
                     },
                     {
                         "label": "鹤壁市",
                         "value": "7008"
                     },
                     {
                         "label": "三门峡市",
                         "value": "7009"
                     },
                     {
                         "label": "商丘市",
                         "value": "7010"
                     },
                     {
                         "label": "许昌市",
                         "value": "7011"
                     },
                     {
                         "label": "漯河市",
                         "value": "7012"
                     },
                     {
                         "label": "平顶山市",
                         "value": "7013"
                     },
                     {
                         "label": "驻马店市",
                         "value": "7014"
                     },
                     {
                         "label": "周口市",
                         "value": "7015"
                     },
                     {
                         "label": "南阳市",
                         "value": "7016"
                     },
                     {
                         "label": "信阳市",
                         "value": "7017"
                     },
                     {
                         "label": "济源市",
                         "value": "7018"
                     },
                     {
                         "label": "武汉市",
                         "value": "7101"
                     },
                     {
                         "label": "黄石市",
                         "value": "7102"
                     },
                     {
                         "label": "襄阳市",
                         "value": "7103"
                     },
                     {
                         "label": "十堰市",
                         "value": "7104"
                     },
                     {
                         "label": "荆州市",
                         "value": "7105"
                     },
                     {
                         "label": "宜昌市",
                         "value": "7106"
                     },
                     {
                         "label": "荆门市",
                         "value": "7107"
                     },
                     {
                         "label": "鄂州市",
                         "value": "7108"
                     },
                     {
                         "label": "孝感市",
                         "value": "7109"
                     },
                     {
                         "label": "黄冈市",
                         "value": "7110"
                     },
                     {
                         "label": "咸宁市",
                         "value": "7111"
                     },
                     {
                         "label": "随州市",
                         "value": "7112"
                     },
                     {
                         "label": "恩施",
                         "value": "7113"
                     },
                     {
                         "label": "潜江市",
                         "value": "7114"
                     },
                     {
                         "label": "仙桃市",
                         "value": "7115"
                     },
                     {
                         "label": "天门市",
                         "value": "7116"
                     },
                     {
                         "label": "神农架林区",
                         "value": "7117"
                     },
                     {
                         "label": "长沙市",
                         "value": "7201"
                     },
                     {
                         "label": "株洲市",
                         "value": "7202"
                     },
                     {
                         "label": "湘潭市",
                         "value": "7203"
                     },
                     {
                         "label": "衡阳市",
                         "value": "7204"
                     },
                     {
                         "label": "益阳市",
                         "value": "7205"
                     },
                     {
                         "label": "常德市",
                         "value": "7206"
                     },
                     {
                         "label": "岳阳市",
                         "value": "7207"
                     },
                     {
                         "label": "邵阳市",
                         "value": "7208"
                     },
                     {
                         "label": "郴州市",
                         "value": "7209"
                     },
                     {
                         "label": "娄底市",
                         "value": "7210"
                     },
                     {
                         "label": "永州市",
                         "value": "7211"
                     },
                     {
                         "label": "怀化市",
                         "value": "7212"
                     },
                     {
                         "label": "张家界市",
                         "value": "7213"
                     },
                     {
                         "label": "湘西",
                         "value": "7214"
                     },
                     {
                         "label": "西安市",
                         "value": "8001"
                     },
                     {
                         "label": "宝鸡市",
                         "value": "8002"
                     },
                     {
                         "label": "咸阳市",
                         "value": "8003"
                     },
                     {
                         "label": "渭南市",
                         "value": "8004"
                     },
                     {
                         "label": "延安市",
                         "value": "8005"
                     },
                     {
                         "label": "榆林市",
                         "value": "8006"
                     },
                     {
                         "label": "铜川市",
                         "value": "8007"
                     },
                     {
                         "label": "汉中市",
                         "value": "8008"
                     },
                     {
                         "label": "安康市",
                         "value": "8009"
                     },
                     {
                         "label": "商洛市",
                         "value": "8010"
                     },
                     {
                         "label": "杨凌",
                         "value": "8011"
                     },
                     {
                         "label": "西宁市",
                         "value": "8101"
                     },
                     {
                         "label": "海东地区",
                         "value": "8102"
                     },
                     {
                         "label": "海南州",
                         "value": "8103"
                     },
                     {
                         "label": "海北州",
                         "value": "8104"
                     },
                     {
                         "label": "海西蒙古族州",
                         "value": "8105"
                     },
                     {
                         "label": "黄南州",
                         "value": "8106"
                     },
                     {
                         "label": "果洛州",
                         "value": "8107"
                     },
                     {
                         "label": "玉树州",
                         "value": "8108"
                     },
                     {
                         "label": "银川市",
                         "value": "8201"
                     },
                     {
                         "label": "石嘴山市",
                         "value": "8202"
                     },
                     {
                         "label": "吴忠市",
                         "value": "8203"
                     },
                     {
                         "label": "固原市",
                         "value": "8204"
                     },
                     {
                         "label": "中卫市",
                         "value": "8205"
                     },
                     {
                         "label": "乌鲁木齐市",
                         "value": "8301"
                     },
                     {
                         "label": "伊犁州",
                         "value": "8302"
                     },
                     {
                         "label": "阿勒泰地区",
                         "value": "8303"
                     },
                     {
                         "label": "塔城地区",
                         "value": "8304"
                     },
                     {
                         "label": "博尔塔拉",
                         "value": "8305"
                     },
                     {
                         "label": "昌吉",
                         "value": "8306"
                     },
                     {
                         "label": "吐鲁番地区",
                         "value": "8307"
                     },
                     {
                         "label": "巴音郭楞",
                         "value": "8308"
                     },
                     {
                         "label": "哈密地区",
                         "value": "8309"
                     },
                     {
                         "label": "和田地区",
                         "value": "8310"
                     },
                     {
                         "label": "阿克苏地区",
                         "value": "8311"
                     },
                     {
                         "label": "克孜勒苏",
                         "value": "8312"
                     },
                     {
                         "label": "喀什地区",
                         "value": "8313"
                     },
                     {
                         "label": "克拉玛依市",
                         "value": "8314"
                     },
                     {
                         "label": "石河子市",
                         "value": "8315"
                     },
                     {
                         "label": "五家渠市",
                         "value": "8316"
                     },
                     {
                         "label": "阿拉尔市",
                         "value": "8317"
                     },
                     {
                         "label": "图木舒克市",
                         "value": "8318"
                     },
                     {
                         "label": "兰州市",
                         "value": "8401"
                     },
                     {
                         "label": "天水市",
                         "value": "8402"
                     },
                     {
                         "label": "嘉峪关市",
                         "value": "8403"
                     },
                     {
                         "label": "武威市",
                         "value": "8404"
                     },
                     {
                         "label": "金昌市",
                         "value": "8405"
                     },
                     {
                         "label": "酒泉市",
                         "value": "8406"
                     },
                     {
                         "label": "张掖市",
                         "value": "8407"
                     },
                     {
                         "label": "庆阳市",
                         "value": "8408"
                     },
                     {
                         "label": "平凉市",
                         "value": "8409"
                     },
                     {
                         "label": "白银市",
                         "value": "8410"
                     },
                     {
                         "label": "定西市",
                         "value": "8411"
                     },
                     {
                         "label": "陇南市",
                         "value": "8412"
                     },
                     {
                         "label": "临夏",
                         "value": "8413"
                     },
                     {
                         "label": "甘南州",
                         "value": "8414"
                     }
                 ],//城市数据
                 rules: {
                     Region: [
                         { type: 'string', required: true,message: '必填', trigger: 'blur' },
                     ],

                 },
             }
        },
        methods:{
            checkedProvince(value){
                this.selectProvince = [];
                for(var i = 0;i<value.length;i++){
                    for(var j = 0;j<this.provinceOptions.length;j++){
                        if(this.provinceOptions[j].value == value[i]){
                            if(value[i] == ''){
                                this.cityArr = [{'value':'','label':'全国'}];
                            }
                            else if(value[i] == '93'){
                                this.cityArr = [{'value':'93','label':'国外'}];
                            }
                            else if(value[i] == '10'){
                                this.cityArr = [{'value':'10','label':'北京市'}];
                            }
                            else if(value[i] == '11'){
                                this.cityArr = [{'value':'11','label':'天津市'}];
                            }
                            else if(value[i] == '30'){
                                this.cityArr = [{'value':'30','label':'上海市'}];
                            }
                            else if(value[i] == '60'){
                                this.cityArr = [{'value':'60','label':'重庆市'}];
                            }
                            else{
                                this.cityArr = this.provinceOptions[j].children;
                            }
                            this.selectProvince.push.apply(this.selectProvince,this.cityArr);
                        }
                    }
                }
            },
            checkedCity(value){
                var arr = [];
                this.selectedAreaList = '';
                this.dialogForm.selectedArea = [];
                for (var i=0;i<value.length;i++){
                    for(var j=0;j<this.cityOptions.length;j++){
                        if(value[i] == this.cityOptions[j].value){
                            arr = [{'value':this.cityOptions[j].value,'label':this.cityOptions[j].label}];
                            this.dialogForm.selectedArea.push.apply(this.dialogForm.selectedArea,arr);
                            this.selectedAreaList = this.selectedAreaList + this.cityOptions[j].label + '，';
                        }
                    }
                }
            },
            getInfoProvince(arr){
                this.dialogForm.citys = arr;
            },
            selectArea(){
                this.form.areaList = this.selectedAreaList;
                this.form.Region = this.dialogForm.selectedArea;
                this.dialogVisible = false;
            },
        }
    }
</script>
