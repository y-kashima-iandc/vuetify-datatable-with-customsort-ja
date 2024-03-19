<script lang="ts">
  const stringCollator = new Intl.Collator("ja", { sensitivity: 'accent', usage: 'sort' });
  const isEmpty = (val: any) => {
    return val === null || val === undefined || (typeof val === 'string' && val.trim() === '')
  };
  type Member = {
    number: number;
    name: string;
    ruby: string;
    originalName: string;
    exist: string;
  }
  const sortName = (sortA: Member, sortB: Member) => {
    const [rubyA, rubyB] = [sortA.ruby, sortB.ruby].map(s => s != null ? s.toString().toLocaleLowerCase() : s);
    if (rubyA === rubyB) return 0;
    if (isEmpty(rubyA) && isEmpty(rubyB)) return 0;
    if (isEmpty(rubyA)) return -1;
    if (isEmpty(rubyB)) return 1;
    return stringCollator.compare(rubyA, rubyB);
  };
  type Header = {
    readonly title?: string;
    readonly align?: "center" | "end" | "start";
    readonly width?: string | number | undefined;
    readonly sortable: boolean;
    readonly key?: string;
    readonly sortRaw?: (a: any, b: any) => number;
  };
  export default {
    data () {
      const headers: readonly Header[] = [
          {
            title: 'No.',
            align: 'center',
            width: 45,
            sortable: false,
            key: 'number',
          },
          {
            title: '武将名',
            align: 'start',
            sortable: true,
            key: 'name',
            sortRaw: sortName,
          },
          {
            title: '元の名',
            sortable: false,
            key: 'originalName'
          },
          {
            title: '人物の信憑性',
            sortable: true,
            key: 'exist'
          },
        ];
      const members: Member[] = [
          {
            number: 1,
            name: '山中鹿之助',
            ruby: 'ヤマナカシカノスケ',
            originalName: '',
            exist: '実在する',
          },
          {
            number: 2,
            name: '大谷古猪之助',
            ruby: 'オオタニコイノスケ',
            originalName: '大谷猪之助',
            exist: '',
          },
          {
            number: 3,
            name: '早川鮎之助',
            ruby: 'ハヤカワアユノスケ',
            originalName: '吉田七助',
            exist: '',
          },
          {
            number: 4,
            name: '横道兵庫之助',
            ruby: 'ヨコミチヒョウゴノスケ',
            originalName: '不明',
            exist: '実在する',
          },
          {
            number: 5,
            name: '寺本生死之助',
            ruby: 'テラモトセイシノスケ',
            originalName: '寺元半四郎',
            exist: '実在の可能性がある',
          },
          {
            number: 6,
            name: '皐月早苗之助',
            ruby: 'サツキサナエノスケ',
            originalName: '不明',
            exist: '実在の可能性がある',
          },
          {
            number: 7,
            name: '高橋渡之助',
            ruby: 'タカハシワタリノスケ',
            originalName: '不明',
            exist: '',
          },
          {
            number: 8,
            name: '秋宅庵之助',
            ruby: 'アキヤケイオリノスケ',
            originalName: '秋宅甚助',
            exist: '実在する',
          },
          {
            number: 9,
            name: '薮中茨之助',
            ruby: 'ヤブナカイバラノスケ',
            originalName: '藪中卯之助',
            exist: '実在の可能性がある',
          },
          {
            number: 10,
            name: '荒波碇之助',
            ruby: 'アラナミイカリノスケ',
            originalName: '徳蔵',
            exist: '',
          },
        ];
      return {
        headers: headers,
        members: members,
      };
    },
  }
</script>

<template>
  <v-app>
    <v-sheet
      class="pa-2"
      width="700"
    >
      <v-data-table
        :headers="headers"
        :items="members"
      ></v-data-table>
    </v-sheet>
  </v-app>
</template>

<style scoped>
</style>
