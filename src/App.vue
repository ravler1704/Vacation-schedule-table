<template>
  <div id="app">
    <table class="vacation_table">
      <thead>
        <tr>
          <th>Employees</th>
          <template v-for="y in years">
            <template v-for="m in y.monthes">
              <th :colspan="m.days.length">{{ m.name }} {{ y.name }}</th>
            </template>
          </template>
        </tr>
        <tr>
          <th></th>
          <template v-for="y in years">
            <template v-for="m in y.monthes">
              <template v-for="d in m.days">
                <th>{{ d.name }}</th>
              </template>
            </template>
          </template>
        </tr>
        <tr>
          <th></th>
          <template v-for="y in years">
            <template v-for="m in y.monthes">
              <template v-for="d in m.days">
                <th>{{ d.date.slice(-2) }}</th>
              </template>
            </template>
          </template>
        </tr>
      </thead>

      <tbody>
        <template v-for="p in getLinearPersons()">
          <tr
            v-if="
              levelIsOpen(p.parentLevelIndex) ||
              isFirstLevel(p.levelIndex) ||
              manualFiltredPersons.length > 0
            "
          >
            <th @click="toggleSubordinates(p.levelIndex, p.subordinatesIsOpen)">
              <div class="fullname_row">
                <span v-html="getPersonNameWithSpaces(p)"></span>
                <span
                  v-if="
                    p.subordinates.length > 0 &&
                    manualFiltredPersons.length === 0
                  "
                  v-html="getArrow(p)"
                  class="arrow"
                ></span>
              </div>
            </th>
            <template v-for="y in years">
              <template v-for="m in y.monthes">
                <template v-for="d in m.days">
                  <td
                    :style="{ backgroundColor: getVacationColor(y, m, d, p) }"
                  >
                    <div v-if="getDayValue(y, m, d, p)" class="tooltip">
                      <span class="tooltiptext">{{
                        getDayTitle(y, m, d, p)
                      }}</span>
                      <span class="tooltipbox">{{
                        getDayValue(y, m, d, p)
                      }}</span>
                    </div>
                  </td>
                </template>
              </template>
            </template>
          </tr>
        </template>
      </tbody>
    </table>
  </div>
</template>

<script>
export default {
  name: "App",
  data: {
    years: [
      {
        name: 2024,
        monthes: [
          {
            name: "Январь",
            days: [
              {
                name: "пн",
                isDayOff: 0,
                date: "2024-01-01",
              },
              {
                name: "вт",
                isDayOff: 0,
                date: "2024-01-02",
              },
              {
                name: "ср",
                isDayOff: 0,
                date: "2024-01-03",
              },
              {
                name: "чт",
                isDayOff: 0,
                date: "2024-01-04",
              },
              {
                name: "пт",
                isDayOff: 0,
                date: "2024-01-05",
              },
              {
                name: "сб",
                isDayOff: 1,
                date: "2024-01-06",
              },
              {
                name: "вс",
                isDayOff: 1,
                date: "2024-01-07",
              },
              {
                name: "пн",
                isDayOff: 0,
                date: "2024-01-08",
              },
              {
                name: "вт",
                isDayOff: 0,
                date: "2024-01-09",
              },
              {
                name: "ср",
                isDayOff: 0,
                date: "2024-01-10",
              },
              {
                name: "чт",
                isDayOff: 0,
                date: "2024-01-11",
              },
              {
                name: "пт",
                isDayOff: 0,
                date: "2024-01-12",
              },
              {
                name: "сб",
                isDayOff: 1,
                date: "2024-01-13",
              },
              {
                name: "вс",
                isDayOff: 1,
                date: "2024-01-14",
              },
              {
                name: "пн",
                isDayOff: 0,
                date: "2024-01-15",
              },
              {
                name: "вт",
                isDayOff: 0,
                date: "2024-01-16",
              },
              {
                name: "ср",
                isDayOff: 0,
                date: "2024-01-17",
              },
              {
                name: "чт",
                isDayOff: 0,
                date: "2024-01-18",
              },
              {
                name: "пт",
                isDayOff: 0,
                date: "2024-01-19",
              },
              {
                name: "сб",
                isDayOff: 1,
                date: "2024-01-20",
              },
              {
                name: "вс",
                isDayOff: 1,
                date: "2024-01-21",
              },
              {
                name: "пн",
                isDayOff: 0,
                date: "2024-01-22",
              },
              {
                name: "вт",
                isDayOff: 0,
                date: "2024-01-23",
              },
              {
                name: "ср",
                isDayOff: 0,
                date: "2024-01-24",
              },
              {
                name: "чт",
                isDayOff: 0,
                date: "2024-01-25",
              },
              {
                name: "пт",
                isDayOff: 0,
                date: "2024-01-26",
              },
              {
                name: "сб",
                isDayOff: 1,
                date: "2024-01-27",
              },
              {
                name: "вс",
                isDayOff: 1,
                date: "2024-01-28",
              },
            ],
          },
          {
            name: "Февраль",
            days: [
              {
                name: "пн",
                isDayOff: 0,
                date: "2024-02-01",
              },
              {
                name: "вт",
                isDayOff: 0,
                date: "2024-02-02",
              },
              {
                name: "ср",
                isDayOff: 0,
                date: "2024-02-03",
              },
              {
                name: "чт",
                isDayOff: 0,
                date: "2024-02-04",
              },
              {
                name: "пт",
                isDayOff: 0,
                date: "2024-02-05",
              },
              {
                name: "сб",
                isDayOff: 1,
                date: "2024-02-06",
              },
              {
                name: "вс",
                isDayOff: 1,
                date: "2024-02-07",
              },
              {
                name: "пн",
                isDayOff: 0,
                date: "2024-02-08",
              },
              {
                name: "вт",
                isDayOff: 0,
                date: "2024-02-09",
              },
              {
                name: "ср",
                isDayOff: 0,
                date: "2024-02-10",
              },
              {
                name: "чт",
                isDayOff: 0,
                date: "2024-02-11",
              },
              {
                name: "пт",
                isDayOff: 0,
                date: "2024-02-12",
              },
              {
                name: "сб",
                isDayOff: 1,
                date: "2024-02-13",
              },
              {
                name: "вс",
                isDayOff: 1,
                date: "2024-02-14",
              },
              {
                name: "пн",
                isDayOff: 0,
                date: "2024-02-15",
              },
              {
                name: "вт",
                isDayOff: 0,
                date: "2024-02-16",
              },
              {
                name: "ср",
                isDayOff: 0,
                date: "2024-02-17",
              },
              {
                name: "чт",
                isDayOff: 0,
                date: "2024-02-18",
              },
              {
                name: "пт",
                isDayOff: 0,
                date: "2024-02-19",
              },
              {
                name: "сб",
                isDayOff: 1,
                date: "2024-02-20",
              },
              {
                name: "вс",
                isDayOff: 1,
                date: "2024-02-21",
              },
              {
                name: "пн",
                isDayOff: 0,
                date: "2024-02-22",
              },
              {
                name: "вт",
                isDayOff: 0,
                date: "2024-02-23",
              },
              {
                name: "ср",
                isDayOff: 0,
                date: "2024-02-24",
              },
              {
                name: "чт",
                isDayOff: 0,
                date: "2024-02-25",
              },
              {
                name: "пт",
                isDayOff: 0,
                date: "2024-02-26",
              },
              {
                name: "сб",
                isDayOff: 1,
                date: "2024-02-27",
              },
              {
                name: "вс",
                isDayOff: 1,
                date: "2024-02-28",
              },
            ],
          },
        ],
      },
    ],
    persons: [
      {
        name: "Lennon Mcmillan",
        idErfl: 12340,
        vacations: [
          {
            date: "2024-01-04",
            type: "Sick leave",
          },
          {
            date: "2024-01-05",
            type: "Vacation",
          },
          {
            date: "2024-01-06",
            type: "Other schedulable type...",
          },
        ],
        subordinatesIsOpen: false,
        subordinates: [],
      },
      {
        name: "Maryam Baker",
        vacations: [],
        subordinatesIsOpen: false,
        subordinates: [],
      },
      {
        name: "Alys Mooney",
        vacations: [],
        subordinatesIsOpen: false,
        subordinates: [],
      },
      {
        name: "Omar Mcdonald",
        vacations: [],
        subordinatesIsOpen: false,
        subordinates: [
          {
            name: "Kirsten Wallace",
            vacations: [],
            subordinatesIsOpen: false,
            subordinates: [
              {
                name: "Kaitlin Roth",
                vacations: [],
                subordinatesIsOpen: false,
                subordinates: [],
              },
              {
                name: "Douglas Miles",
                vacations: [],
                subordinatesIsOpen: false,
                subordinates: [],
              },
            ],
          },
          {
            name: "Lawrence Richard",
            vacations: [],
            subordinatesIsOpen: false,
            subordinates: [],
          },
        ],
      },
      {
        name: "Saoirse Jordan",
        vacations: [],
        subordinatesIsOpen: false,
        subordinates: [],
      },
      {
        name: "Hallie Oconnor",
        vacations: [],
        subordinatesIsOpen: false,
        subordinates: [],
      },
      {
        name: "Jacob Yates",
        vacations: [],
        subordinatesIsOpen: false,
        subordinates: [],
      },
      {
        name: "Ciara Coffey",
        vacations: [],
        subordinatesIsOpen: false,
        subordinates: [],
      },
    ],
  },
  methods: {
    getPersonNameWithSpaces(person) {
      if (
        this.isFirstLevel(person.levelIndex) ||
        this.manualFiltredPersons.length > 0
      ) {
        return person.name;
      } else {
        const underscoreCount = (
          person.levelIndex.match(new RegExp("_", "g")) || []
        ).length;
        const spaceCount = 2 * (underscoreCount - 1);
        return "&nbsp;".repeat(spaceCount) + person.name;
      }
    },
    getArrow(person) {
      return person.subordinatesIsOpen ? "&#708;" : "&#709;";
    },
    toggleSubordinates(index, isOpen) {
      this.res.find((p) => p.levelIndex === index).subordinatesIsOpen =
        !this.res.find((p) => p.levelIndex === index).subordinatesIsOpen;

      //When collapsing parent element, collapse all children
      if (isOpen) {
        this.res
          .filter((p) => p.levelIndex.indexOf(index) === 0)
          .map((p) => {
            p.subordinatesIsOpen = false;
            return p;
          });
      }
    },
    isFirstLevel(levelIndex) {
      return this.getLevelByIndex(levelIndex) === 1;
    },
    levelIsOpen(index) {
      if (index !== "")
        return this.res.find((p) => p.levelIndex === index).subordinatesIsOpen;
    },
    getLevelByIndex(levelIndex) {
      return (levelIndex.match(/_/g) || []).length;
    },
    getDayValue(y, m, d, p) {
      const res = p.vacations.filter((v) => {
        return v.date === d.date;
      });
      return res[0]?.type?.slice(0, 1);
    },
    getDayTitle(y, m, d, p) {
      const res = p.vacations.filter((v) => {
        return v.date === d.date;
      });
      return res[0]?.type;
    },
    getVacationColor(y, m, d, p) {
      const res = p.vacations.filter((v) => {
        return v.date === d.date;
      });
      return res[0]?.color;
    },
    getList() {
      this.list.map((person, personIndex) => {
        let clonedCalendar = JSON.parse(JSON.stringify(this.calendar));
        this.list[personIndex].dates = [];
      });
    },
    getLinearPersons() {
      return this.manualFiltredPersons.length > 0
        ? this.manualFiltredPersons
        : this.getSubordinates(this.persons, this);
    },
    getSubordinates(persons, context, index = "") {
      const isRootObj = this.persons === persons;
      if (isRootObj && context.res.length > 0) {
        return context.res;
      }
      persons.map((p, pIndex) => {
        if (p.subordinates.length > 0) {
          //write the main element
          p.levelIndex = index + "_" + pIndex;
          p.parentLevelIndex = index;
          context.res.push(p);
          //Write nested elements
          p.subordinates.map((pS, pSIndes) => {
            pS.levelIndex = index + "_" + pIndex + "_" + pSIndes;
            pS.parentLevelIndex = index + "_" + pIndex;
            context.res.push(pS);
            //If a nested element has nested elements
            if (pS.subordinates.length > 0) {
              context.getSubordinates(
                pS.subordinates,
                context,
                index + "_" + pIndex + "_" + pSIndes
              );
            }
          });
        } else {
          p.levelIndex = index + "_" + pIndex;
          p.parentLevelIndex = index;
          context.res.push(p);
        }
      });

      return context.res;
    },
    setManualFiltredPersons(obj) {
      this.manualFiltredPersons = obj;
    },
  },
  data() {
    return {
      res: [],
      manualFiltredPersons: [],
      years: [
        {
          name: 2024,
          monthes: [
            {
              name: "January",
              days: [
                {
                  name: "mo",
                  isDayOff: 0,
                  date: "2024-01-01",
                },
                {
                  name: "tu",
                  isDayOff: 0,
                  date: "2024-01-02",
                },
                {
                  name: "we",
                  isDayOff: 0,
                  date: "2024-01-03",
                },
                {
                  name: "th",
                  isDayOff: 0,
                  date: "2024-01-04",
                },
                {
                  name: "fr",
                  isDayOff: 0,
                  date: "2024-01-05",
                },
                {
                  name: "sa",
                  isDayOff: 1,
                  date: "2024-01-06",
                },
                {
                  name: "su",
                  isDayOff: 1,
                  date: "2024-01-07",
                },
                {
                  name: "mo",
                  isDayOff: 0,
                  date: "2024-01-08",
                },
                {
                  name: "tu",
                  isDayOff: 0,
                  date: "2024-01-09",
                },
                {
                  name: "we",
                  isDayOff: 0,
                  date: "2024-01-10",
                },
                {
                  name: "th",
                  isDayOff: 0,
                  date: "2024-01-11",
                },
                {
                  name: "fr",
                  isDayOff: 0,
                  date: "2024-01-12",
                },
                {
                  name: "sa",
                  isDayOff: 1,
                  date: "2024-01-13",
                },
                {
                  name: "su",
                  isDayOff: 1,
                  date: "2024-01-14",
                },
                {
                  name: "mo",
                  isDayOff: 0,
                  date: "2024-01-15",
                },
                {
                  name: "tu",
                  isDayOff: 0,
                  date: "2024-01-16",
                },
                {
                  name: "we",
                  isDayOff: 0,
                  date: "2024-01-17",
                },
                {
                  name: "th",
                  isDayOff: 0,
                  date: "2024-01-18",
                },
                {
                  name: "fr",
                  isDayOff: 0,
                  date: "2024-01-19",
                },
                {
                  name: "sa",
                  isDayOff: 1,
                  date: "2024-01-20",
                },
                {
                  name: "su",
                  isDayOff: 1,
                  date: "2024-01-21",
                },
                {
                  name: "mo",
                  isDayOff: 0,
                  date: "2024-01-22",
                },
                {
                  name: "tu",
                  isDayOff: 0,
                  date: "2024-01-23",
                },
                {
                  name: "we",
                  isDayOff: 0,
                  date: "2024-01-24",
                },
                {
                  name: "th",
                  isDayOff: 0,
                  date: "2024-01-25",
                },
                {
                  name: "fr",
                  isDayOff: 0,
                  date: "2024-01-26",
                },
                {
                  name: "sa",
                  isDayOff: 1,
                  date: "2024-01-27",
                },
                {
                  name: "su",
                  isDayOff: 1,
                  date: "2024-01-28",
                },
              ],
            },
            {
              name: "February",
              days: [
                {
                  name: "mo",
                  isDayOff: 0,
                  date: "2024-02-01",
                },
                {
                  name: "tu",
                  isDayOff: 0,
                  date: "2024-02-02",
                },
                {
                  name: "we",
                  isDayOff: 0,
                  date: "2024-02-03",
                },
                {
                  name: "th",
                  isDayOff: 0,
                  date: "2024-02-04",
                },
                {
                  name: "fr",
                  isDayOff: 0,
                  date: "2024-02-05",
                },
                {
                  name: "sa",
                  isDayOff: 1,
                  date: "2024-02-06",
                },
                {
                  name: "su",
                  isDayOff: 1,
                  date: "2024-02-07",
                },
                {
                  name: "mo",
                  isDayOff: 0,
                  date: "2024-02-08",
                },
                {
                  name: "tu",
                  isDayOff: 0,
                  date: "2024-02-09",
                },
                {
                  name: "we",
                  isDayOff: 0,
                  date: "2024-02-10",
                },
                {
                  name: "th",
                  isDayOff: 0,
                  date: "2024-02-11",
                },
                {
                  name: "fr",
                  isDayOff: 0,
                  date: "2024-02-12",
                },
                {
                  name: "sa",
                  isDayOff: 1,
                  date: "2024-02-13",
                },
                {
                  name: "su",
                  isDayOff: 1,
                  date: "2024-02-14",
                },
                {
                  name: "mo",
                  isDayOff: 0,
                  date: "2024-02-15",
                },
                {
                  name: "tu",
                  isDayOff: 0,
                  date: "2024-02-16",
                },
                {
                  name: "we",
                  isDayOff: 0,
                  date: "2024-02-17",
                },
                {
                  name: "th",
                  isDayOff: 0,
                  date: "2024-02-18",
                },
                {
                  name: "fr",
                  isDayOff: 0,
                  date: "2024-02-19",
                },
                {
                  name: "sa",
                  isDayOff: 1,
                  date: "2024-02-20",
                },
                {
                  name: "su",
                  isDayOff: 1,
                  date: "2024-02-21",
                },
                {
                  name: "mo",
                  isDayOff: 0,
                  date: "2024-02-22",
                },
                {
                  name: "tu",
                  isDayOff: 0,
                  date: "2024-02-23",
                },
                {
                  name: "we",
                  isDayOff: 0,
                  date: "2024-02-24",
                },
                {
                  name: "th",
                  isDayOff: 0,
                  date: "2024-02-25",
                },
                {
                  name: "fr",
                  isDayOff: 0,
                  date: "2024-02-26",
                },
                {
                  name: "sa",
                  isDayOff: 1,
                  date: "2024-02-27",
                },
                {
                  name: "su",
                  isDayOff: 1,
                  date: "2024-02-28",
                },
              ],
            },
          ],
        },
      ],
      persons: [
        {
          name: "Lennon Mcmillan",
          vacations: [
            {
              date: "2024-01-04",
              type: "Sick leave",
            },
            {
              date: "2024-01-05",
              type: "Vacation",
            },
            {
              date: "2024-01-06",
              type: "Other schedulable type...",
            },
          ],
          subordinatesIsOpen: false,
          subordinates: [],
        },
        {
          name: "Maryam Baker",
          idErfl: 12341,
          vacations: [],
          subordinatesIsOpen: false,
          subordinates: [],
        },
        {
          name: "Alys Mooney",
          idErfl: 12342,
          vacations: [],
          subordinatesIsOpen: false,
          subordinates: [],
        },
        {
          name: "Omar Mcdonald",
          idErfl: 12343,
          vacations: [],
          subordinatesIsOpen: false,
          subordinates: [
            {
              name: "Kirsten Wallace",
              idErfl: 12344,
              vacations: [],
              subordinatesIsOpen: false,
              subordinates: [
                {
                  name: "Kaitlin Roth",
                  idErfl: 12344,
                  vacations: [],
                  subordinatesIsOpen: false,
                  subordinates: [],
                },
                {
                  name: "Douglas Miles",
                  idErfl: 12345,
                  vacations: [
                    {
                      date: "2024-01-04",
                      type: "Sick leave",
                    },
                  ],
                  subordinatesIsOpen: false,
                  subordinates: [],
                },
              ],
            },
            {
              name: "Lawrence Richard",
              idErfl: 12345,
              vacations: [],
              subordinatesIsOpen: false,
              subordinates: [],
            },
          ],
        },
        {
          name: "Saoirse Jordan",
          idErfl: 12346,
          vacations: [],
          subordinatesIsOpen: false,
          subordinates: [],
        },
        {
          name: "Hallie Oconnor",
          idErfl: 12347,
          vacations: [],
          subordinatesIsOpen: false,
          subordinates: [],
        },
        {
          name: "Jacob Yates",
          idErfl: 12348,
          vacations: [],
          subordinatesIsOpen: false,
          subordinates: [],
        },
        {
          name: "Ciara Coffey",
          idErfl: 12349,
          vacations: [],
          subordinatesIsOpen: false,
          subordinates: [],
        },
      ],
    };
  },
};
</script>
<style scoped>
table,
th,
td {
  font-weight: normal;
  text-align: left;
  border-collapse: collapse;
}

th,
td {
  padding: 5px;
  border: 1px solid #b8b8b8;
}

tr:hover {
  background-color: rgba(18, 26, 81, 0.22);
}

td:hover::after {
  background-color: rgba(18, 26, 81, 0.22);
}

.vacation_table {
  width: 100%;
  width: -moz-available; /* WebKit-based browsers will ignore this. */
  width: -webkit-fill-available; /* Mozilla-based browsers will ignore this. */
  width: fill-available;
}

.arrow {
  border: 1px solid green;
  margin-left: 10px;
  border-radius: 10px;
  background-color: white;
  padding-left: 5px;
  padding-right: 5px;
  cursor: pointer;
  color: black;
  font-weight: bold;
}
.fullname_row {
  white-space: nowrap;
  display: flex;
  justify-content: space-between;
}

.fio_filter {
  min-width: 300px;
  width: fit-content;
}

table {
  display: block;
  overflow-x: auto;
  white-space: nowrap;
  tr > th:first-child,
  tr > td:first-child {
    z-index: 2;
    position: sticky;
    left: 0;
    background-color: #d6deed;
    border-left: 10px;
  }
}

#container {
  width: 100%;
  margin: 0;
  padding: 0;
  background-color: #ebf1ff;
}

#container-header {
  display: flex;
  align-items: center;
  justify-content: center;
  color: #fff;
  font-size: 20px;
  border-radius: 8px 8px 0 0;
  min-height: 50pt;
  background: linear-gradient(90deg, rgb(18, 26, 75) 0%, rgb(18 26 81) 100%);
}

.tooltip {
  position: relative;
  display: inline-block;
  border: none;
}

.tooltip .tooltipbox {
  cursor: pointer;
  padding: 5px;
}

.tooltip .tooltiptext {
  top: -30px;
  left: 20px;
  visibility: hidden;
  opacity: 0;
  transition: visibility 0.3s linear, opacity 0.3s linear;
  background-color: black;
  color: #fff;
  text-align: center;
  border-radius: 6px;
  padding: 5px;
  cursor: pointer;
  /* Position the tooltip */
  position: absolute;
  z-index: 1;
}

.tooltip:hover .tooltiptext {
  visibility: visible;
  opacity: 1;
  transition: visibility 0.3s linear, opacity 0.3s linear;
}
</style>
