<template>
<div>
    <a-row>
      <a-col :span="18">
          <a-page-header style="border: 1px solid rgb(235, 237, 240)" title="Agenda del día" s/>
        <a-table :columns="columns" :data-source="data" bordered :style="{ padding: '5%', background: 'white'}">
            <template slot="name" slot-scope="text">
            <a>{{ text }}</a>
            </template>

        </a-table>
        <div style="position: sticky;">
          <a-button :size="large">Pendientes</a-button>
          <a-button :size="large">En curso</a-button>
          <a-button :size="large">Cerrados</a-button>
        </div>
      </a-col>
      <a-col :span="6">
        <div style="width: 300px; border: 1px solid #d9d9d9; border-radius: 4px">
        <a-calendar :fullscreen="false" :header-render="headerRender" @panelChange="onPanelChange" :style="{ padding: '5%', background: 'white'}" />
        </div>
        <a-button type="primary" size='large' @click="() => setModal1Visible(true)" style="position: fixed; bottom: 10%; right: 5%;">
          <a-icon type="plus"/>
        </a-button>
        <a-modal
          title="20px to Top"
          :dialog-style="{ top: '20px' }"
          :visible="modal1Visible"
          @ok="() => setModal1Visible(false)"
          @cancel="() => setModal1Visible(false)"
        >
          <p>some contents...</p>
          <p>some contents...</p>
          <p>some contents...</p>
        </a-modal>
      </a-col>
    </a-row>
</div>
    
</template>

<script>
const columns = [
  {
    title: 'Aseguradora',
    dataIndex: 'name',
    scopedSlots: { customRender: 'name' },
  },
  {
    title: 'Asegurado',
    dataIndex: 'money',
  },
  {
    title: 'Juzgado',
    dataIndex: 'address',
  },
];

const data = [
  {
    key: '1',
    name: 'John Brown',
    money: '￥300,000.00',
    address: 'New York No. 1 Lake Park',
  },
  {
    key: '2',
    name: 'Jim Green',
    money: '￥1,256,000.00',
    address: 'London No. 1 Lake Park',
  },
  {
    key: '3',
    name: 'Joe Black',
    money: '￥120,000.00',
    address: 'Sidney No. 1 Lake Park',
  },
];

export default {
    data() {
    return {
      modal1Visible: false,
      data,
      columns,
    };
  },
    layout: 'logged',
    methods: {
      setModal1Visible(modal1Visible) {
      this.modal1Visible = modal1Visible;
    },
    onPanelChange(value, mode) {
      // eslint-disable-next-line no-console
      console.log(value, mode);
    },
    headerRender({ value, type, onChange, onTypeChange }) {
      const start = 0;
      const end = 12;
      const monthOptions = [];

      const current = value.clone();
      const localeData = value.localeData();
      const months = [];
      for (let i = 0; i < 12; i++) {
        current.month(i);
        months.push(localeData.monthsShort(current));
      }

      for (let index = start; index < end; index++) {
        monthOptions.push(
          <a-select-option class="month-item" key={`${index}`}>
            {months[index]}
          </a-select-option>,
        );
      }
      const month = value.month();

      const year = value.year();
      const options = [];
      for (let i = year - 10; i < year + 10; i += 1) {
        options.push(
          <a-select-option key={i} value={i} class="year-item">
            {i}
          </a-select-option>,
        );
      }
      return (
        <div style={{ padding: '10px' }}>
          <div style={{ marginBottom: '10px' }}>Custom header </div>
          <a-row type="flex" justify="space-between">
            <a-col>
              <a-radio-group size="small" onChange={e => onTypeChange(e.target.value)} value={type}>
                <a-radio-button value="month">Month</a-radio-button>
                <a-radio-button value="year">Year</a-radio-button>
              </a-radio-group>
            </a-col>
            <a-col>
              <a-select
                size="small"
                dropdownMatchSelectWidth={false}
                class="my-year-select"
                onChange={newYear => {
                  const now = value.clone().year(newYear);
                  onChange(now);
                }}
                value={String(year)}
              >
                {options}
              </a-select>
            </a-col>
            <a-col>
              <a-select
                size="small"
                dropdownMatchSelectWidth={false}
                value={String(month)}
                onChange={selectedMonth => {
                  const newValue = value.clone();
                  newValue.month(parseInt(selectedMonth, 10));
                  onChange(newValue);
                }}
              >
                {monthOptions}
              </a-select>
            </a-col>
          </a-row>
        </div>
      );
    },
  },

}
</script>

<style>

</style>