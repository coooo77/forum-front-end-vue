<template>
  <div class="container py-5">
    <UserEditCard :initial-user-profile="profile" @after-submit="handleAfterSubmit" />
    <hr />
  </div>
</template>

<script>
import UserEditCard from "../components/UserEditCard";
const dummyData = {
  profile: {
    id: 3,
    name: "user2",
    email: "user2@example.com",
    password: "$2a$10$VHKmtPqbcUzK46qxLllqj.w506U2N2TObMmnpdlNG2CLZPa1xzuTi",
    isAdmin: true,
    image: "https://i.imgur.com/IaCnj2S.jpg",
    createdAt: "2020-02-28T14:38:32.000Z",
    updatedAt: "2020-04-21T09:44:01.000Z",
    Comments: [
      {
        id: 5,
        text: "Et est asperiores eaque accusantium voluptas.",
        UserId: 3,
        RestaurantId: 5,
        createdAt: "2020-02-28T14:38:32.000Z",
        updatedAt: "2020-02-28T14:38:32.000Z",
        Restaurant: {
          id: 5,
          name: "Mitchel Beatty",
          tel: "171-324-8413",
          address: "85408 Francisca Square",
          opening_hours: "08:00",
          description:
            "Aut cumque excepturi exercitationem libero voluptates impedit. Enim animi repellendus tempora doloremque. Esse in delectus sequi ullam sed animi.",
          image: "https://i.imgur.com/awJFBLn.jpg",
          viewCounts: 276,
          createdAt: "2020-02-28T14:38:32.000Z",
          updatedAt: "2020-05-21T10:34:24.000Z",
          CategoryId: 3
        }
      },
      {
        id: 11,
        text: "In rem dolorem impedit sit.",
        UserId: 3,
        RestaurantId: 11,
        createdAt: "2020-02-28T14:38:32.000Z",
        updatedAt: "2020-02-28T14:38:32.000Z",
        Restaurant: {
          id: 11,
          name: "Vergie Considine",
          tel: "351.951.8030 x0330",
          address: "8865 Conrad Mill",
          opening_hours: "08:00",
          description:
            "Quia omnis natus est praesentium dolores aliquid debitis omnis molestias.",
          image:
            "https://loremflickr.com/320/240/restaurant,food/?random=0.7508871784973614",
          viewCounts: 1,
          createdAt: "2020-02-28T14:38:32.000Z",
          updatedAt: "2020-03-09T06:09:15.000Z",
          CategoryId: 5
        }
      },
      {
        id: 12,
        text: "Est omnis fugiat tempore sint voluptatem nam.",
        UserId: 3,
        RestaurantId: 12,
        createdAt: "2020-02-28T14:38:32.000Z",
        updatedAt: "2020-02-28T14:38:32.000Z",
        Restaurant: {
          id: 12,
          name: "Oliver Padberg",
          tel: "865-523-0270 x58016",
          address: "771 Oberbrunner Hollow",
          opening_hours: "08:00",
          description:
            "Magni qui facilis asperiores. Voluptatem cumque corrupti ea at voluptatem. Assumenda esse esse fuga autem dolor qui. Veniam qui eius vero magnam ut inventore magni est.",
          image:
            "https://loremflickr.com/320/240/restaurant,food/?random=22.348939427568215",
          viewCounts: 5,
          createdAt: "2020-02-28T14:38:32.000Z",
          updatedAt: "2020-04-10T10:48:16.000Z",
          CategoryId: 1
        }
      },
      {
        id: 16,
        text: "Harum illo molestiae.",
        UserId: 3,
        RestaurantId: 16,
        createdAt: "2020-02-28T14:38:32.000Z",
        updatedAt: "2020-02-28T14:38:32.000Z",
        Restaurant: {
          id: 16,
          name: "Aaliyah Lakin",
          tel: "1-235-923-9473 x43870",
          address: "1951 Jakubowski Villages",
          opening_hours: "08:00",
          description: "quidem",
          image:
            "https://loremflickr.com/320/240/restaurant,food/?random=91.06034163072859",
          viewCounts: 9,
          createdAt: "2020-02-28T14:38:32.000Z",
          updatedAt: "2020-04-11T04:16:08.000Z",
          CategoryId: 5
        }
      },
      {
        id: 21,
        text: "Nostrum aspernatur quia labore.",
        UserId: 3,
        RestaurantId: 21,
        createdAt: "2020-02-28T14:38:32.000Z",
        updatedAt: "2020-02-28T14:38:32.000Z",
        Restaurant: {
          id: 21,
          name: "Candido Connelly",
          tel: "306-741-4682",
          address: "0922 Lauren Ferry",
          opening_hours: "08:00",
          description:
            "Eos eum voluptatibus dolorem ut. Voluptate qui maxime voluptas veritatis sit. Consequatur eligendi deleniti sed itaque aut.\r\n \r\nSit recusandae ipsam repudiandae laboriosam recusandae harum qui quia dolores. Sit eum aliquid vel voluptas minus voluptatem. Quam sit natus id enim praesentium voluptas. Iste in harum quia culpa magni rerum ea iure.\r\n \r\nCupiditate quasi neque distinctio sed consequatur nulla. Inventore possimus similique beatae. Qui consequatur provident amet eveniet repudiandae sint officia. Nobis non ducimus corporis. Iure dolor corporis.",
          image: "https://i.imgur.com/9r8MUJe.jpg",
          viewCounts: 3707,
          createdAt: "2020-02-28T14:38:32.000Z",
          updatedAt: "2020-03-09T06:12:01.000Z",
          CategoryId: 1
        }
      },
      {
        id: 27,
        text: "Ut dicta facilis accusantium ut.",
        UserId: 3,
        RestaurantId: 27,
        createdAt: "2020-02-28T14:38:32.000Z",
        updatedAt: "2020-02-28T14:38:32.000Z",
        Restaurant: {
          id: 27,
          name: "Ms. Alex Wuckert",
          tel: "(598) 990-0851",
          address: "290 Davis Ferry",
          opening_hours: "08:00",
          description:
            "Consequatur similique earum accusamus. Veritatis facilis non. Architecto sunt velit consequatur cumque rem sit occaecati et beatae. Sequi tenetur in aspernatur labore reprehenderit. Sit velit nulla dolorem aut ea sapiente.",
          image:
            "https://loremflickr.com/320/240/restaurant,food/?random=17.861944116977146",
          viewCounts: 0,
          createdAt: "2020-02-28T14:38:32.000Z",
          updatedAt: "2020-02-28T14:38:32.000Z",
          CategoryId: 1
        }
      },
      {
        id: 28,
        text: "Consequuntur et a.",
        UserId: 3,
        RestaurantId: 28,
        createdAt: "2020-02-28T14:38:32.000Z",
        updatedAt: "2020-02-28T14:38:32.000Z",
        Restaurant: {
          id: 28,
          name: "Damion Muller",
          tel: "(602) 046-4624 x4810",
          address: "3923 Wehner Corner",
          opening_hours: "08:00",
          description: "Fuga at hic reiciendis.",
          image:
            "https://loremflickr.com/320/240/restaurant,food/?random=85.49537442402593",
          viewCounts: 4,
          createdAt: "2020-02-28T14:38:32.000Z",
          updatedAt: "2020-03-31T03:54:27.000Z",
          CategoryId: 5
        }
      },
      {
        id: 30,
        text: "Facilis aut minus.",
        UserId: 3,
        RestaurantId: 30,
        createdAt: "2020-02-28T14:38:32.000Z",
        updatedAt: "2020-02-28T14:38:32.000Z",
        Restaurant: {
          id: 30,
          name: "Nikita Boyer",
          tel: "(284) 625-0408 x71025",
          address: "101 Heidenreich Roads",
          opening_hours: "08:00",
          description:
            "Labore nihil ipsum quibusdam et laboriosam. Libero deleniti doloribus placeat sit velit rerum ipsam ut repudiandae. Aspernatur dolore doloremque eos. Molestiae animi ipsa labore officia.\n \rNon quaerat eos quidem aut quam facilis quia. Veniam soluta et excepturi ratione non eos repudiandae. Eos reprehenderit rerum soluta qui commodi dolorem rerum. Qui impedit unde alias deleniti. Doloremque unde distinctio.\n \rNumquam reiciendis ex pariatur tempore repellat. Perferendis nulla voluptatum et alias. Reiciendis inventore nihil atque et quia. Earum nobis aliquid voluptas error necessitatibus. Qui perspiciatis commodi aut qui est doloribus iure fuga.",
          image:
            "https://loremflickr.com/320/240/restaurant,food/?random=90.49719023698857",
          viewCounts: 0,
          createdAt: "2020-02-28T14:38:32.000Z",
          updatedAt: "2020-02-28T14:38:32.000Z",
          CategoryId: 2
        }
      },
      {
        id: 31,
        text: "Ratione aspernatur et voluptatibus molestias.",
        UserId: 3,
        RestaurantId: 31,
        createdAt: "2020-02-28T14:38:32.000Z",
        updatedAt: "2020-02-28T14:38:32.000Z",
        Restaurant: {
          id: 31,
          name: "Noe Raynor",
          tel: "1-595-633-3163 x052",
          address: "2075 Sharon Rapid",
          opening_hours: "08:00",
          description:
            "Quo voluptatum rerum temporibus enim nihil. Ea vitae odit quis ducimus doloremque veniam ut. Sequi debitis at et voluptas consectetur fugit qui. Vero voluptas quasi sed quam et sit. Atque id maxime voluptas. Dolorem voluptas facilis et odit optio sunt excepturi quaerat pariatur.",
          image:
            "https://loremflickr.com/320/240/restaurant,food/?random=43.066607162000324",
          viewCounts: 2,
          createdAt: "2020-02-28T14:38:32.000Z",
          updatedAt: "2020-04-10T14:30:59.000Z",
          CategoryId: 1
        }
      },
      {
        id: 32,
        text: "Quo placeat voluptates iure ut quia.",
        UserId: 3,
        RestaurantId: 32,
        createdAt: "2020-02-28T14:38:32.000Z",
        updatedAt: "2020-02-28T14:38:32.000Z",
        Restaurant: {
          id: 32,
          name: "Rafael Schaden III",
          tel: "1-836-107-5530",
          address: "7262 Devyn Centers",
          opening_hours: "08:00",
          description:
            "Dicta perspiciatis aliquid voluptate tempore similique.",
          image:
            "https://loremflickr.com/320/240/restaurant,food/?random=2.1540435433775817",
          viewCounts: 0,
          createdAt: "2020-02-28T14:38:32.000Z",
          updatedAt: "2020-02-28T14:38:32.000Z",
          CategoryId: 1
        }
      },
      {
        id: 33,
        text: "Ut enim est ea ea fugiat nisi unde.",
        UserId: 3,
        RestaurantId: 33,
        createdAt: "2020-02-28T14:38:32.000Z",
        updatedAt: "2020-02-28T14:38:32.000Z",
        Restaurant: {
          id: 33,
          name: "Kenny Dach",
          tel: "(647) 053-5104 x9921",
          address: "41601 Lesch Orchard",
          opening_hours: "08:00",
          description:
            "Sequi quo fuga recusandae perspiciatis facere sed et asperiores. In unde id excepturi et repellendus tempore voluptatibus. Et quas et unde. Consequatur quae voluptas dolorem natus odit quis doloribus.",
          image:
            "https://loremflickr.com/320/240/restaurant,food/?random=18.95963061671191",
          viewCounts: 0,
          createdAt: "2020-02-28T14:38:32.000Z",
          updatedAt: "2020-02-28T14:38:32.000Z",
          CategoryId: 5
        }
      },
      {
        id: 35,
        text: "Non doloribus illum quia ut.",
        UserId: 3,
        RestaurantId: 35,
        createdAt: "2020-02-28T14:38:32.000Z",
        updatedAt: "2020-02-28T14:38:32.000Z",
        Restaurant: {
          id: 35,
          name: "Daphnee Lowe",
          tel: "548-757-2237",
          address: "232 Jennings Junctions",
          opening_hours: "08:00",
          description: "id dolores quis",
          image:
            "https://loremflickr.com/320/240/restaurant,food/?random=85.90083920238921",
          viewCounts: 0,
          createdAt: "2020-02-28T14:38:32.000Z",
          updatedAt: "2020-02-28T14:38:32.000Z",
          CategoryId: 4
        }
      },
      {
        id: 42,
        text:
          "Qui labore delectus quo magnam vel quae reiciendis eos asperiores.",
        UserId: 3,
        RestaurantId: 42,
        createdAt: "2020-02-28T14:38:32.000Z",
        updatedAt: "2020-02-28T14:38:32.000Z",
        Restaurant: {
          id: 42,
          name: "Adrian Weimann",
          tel: "(102) 131-9224 x2147",
          address: "04294 Nils Track",
          opening_hours: "08:00",
          description:
            "Et dolores eos sed aut doloribus velit autem quae. Debitis recusandae occaecati ut rerum. Esse dolorum dolorum velit nemo. Culpa mollitia non maxime aspernatur neque aut voluptates architecto.\n \rAnimi veniam nesciunt ut est assumenda voluptatem omnis eligendi. Nam incidunt sint. Reprehenderit et eveniet est laborum ut. Et consequuntur quod ut.\n \rSequi id natus voluptatem repudiandae doloremque pariatur quaerat sit. Quibusdam ipsa voluptatem consequatur at. Illo ullam illum. Enim et cum nulla. Illum debitis et.",
          image:
            "https://loremflickr.com/320/240/restaurant,food/?random=57.71296646754862",
          viewCounts: 2,
          createdAt: "2020-02-28T14:38:32.000Z",
          updatedAt: "2020-03-22T08:10:15.000Z",
          CategoryId: 4
        }
      },
      {
        id: 55,
        text: "Eos facilis facere debitis nam.",
        UserId: 3,
        RestaurantId: 5,
        createdAt: "2020-02-28T14:38:32.000Z",
        updatedAt: "2020-02-28T14:38:32.000Z",
        Restaurant: {
          id: 5,
          name: "Mitchel Beatty",
          tel: "171-324-8413",
          address: "85408 Francisca Square",
          opening_hours: "08:00",
          description:
            "Aut cumque excepturi exercitationem libero voluptates impedit. Enim animi repellendus tempora doloremque. Esse in delectus sequi ullam sed animi.",
          image: "https://i.imgur.com/awJFBLn.jpg",
          viewCounts: 276,
          createdAt: "2020-02-28T14:38:32.000Z",
          updatedAt: "2020-05-21T10:34:24.000Z",
          CategoryId: 3
        }
      },
      {
        id: 56,
        text: "Aspernatur iusto accusantium tempore.",
        UserId: 3,
        RestaurantId: 6,
        createdAt: "2020-02-28T14:38:32.000Z",
        updatedAt: "2020-02-28T14:38:32.000Z",
        Restaurant: {
          id: 6,
          name: "Vicenta Gutkowski Test By Nacho",
          tel: "128-905-3953",
          address: "371 Reuben Vista test",
          opening_hours: "00:00",
          description: "labore",
          image:
            "https://loremflickr.com/320/240/restaurant,food/?random=16.659471621888123",
          viewCounts: 45,
          createdAt: "2020-02-28T14:38:32.000Z",
          updatedAt: "2020-05-19T06:28:37.000Z",
          CategoryId: 2
        }
      },
      {
        id: 59,
        text: "Et repudiandae ipsam incidunt alias ut.",
        UserId: 3,
        RestaurantId: 9,
        createdAt: "2020-02-28T14:38:32.000Z",
        updatedAt: "2020-02-28T14:38:32.000Z",
        Restaurant: {
          id: 9,
          name: "Luz Schaden",
          tel: "1-712-742-4184",
          address: "4929 Wisozk Centers",
          opening_hours: "08:00",
          description:
            "Culpa deserunt molestiae eligendi est ex incidunt.\nNisi sit totam.",
          image:
            "https://loremflickr.com/320/240/restaurant,food/?random=6.497835218728576",
          viewCounts: 31,
          createdAt: "2020-02-28T14:38:32.000Z",
          updatedAt: "2020-04-22T06:18:59.000Z",
          CategoryId: 5
        }
      },
      {
        id: 60,
        text: "Officiis quis blanditiis magni et.",
        UserId: 3,
        RestaurantId: 10,
        createdAt: "2020-02-28T14:38:32.000Z",
        updatedAt: "2020-02-28T14:38:32.000Z",
        Restaurant: {
          id: 10,
          name: "Corbin Gusikowski",
          tel: "(506) 198-3977",
          address: "4747 Lubowitz Brook",
          opening_hours: "08:00",
          description:
            "Aut quia aut ea nostrum quae doloremque necessitatibus. Eos illo quia et. Culpa repellat eos minus necessitatibus aut debitis accusamus.\n \rAssumenda aut itaque corrupti soluta et aut est. Hic non dignissimos odit qui. Optio doloribus rerum molestiae dolorem commodi. Culpa et officiis.\n \rCulpa laborum ea eos praesentium enim quasi eos. Nobis praesentium maxime soluta delectus eveniet reiciendis aut. Voluptates nesciunt et explicabo.",
          image:
            "https://loremflickr.com/320/240/restaurant,food/?random=6.84802493817025",
          viewCounts: 31,
          createdAt: "2020-02-28T14:38:32.000Z",
          updatedAt: "2020-04-11T08:35:22.000Z",
          CategoryId: 5
        }
      },
      {
        id: 61,
        text:
          "Reiciendis nostrum laboriosam voluptatem maxime consequatur numquam saepe.",
        UserId: 3,
        RestaurantId: 11,
        createdAt: "2020-02-28T14:38:32.000Z",
        updatedAt: "2020-02-28T14:38:32.000Z",
        Restaurant: {
          id: 11,
          name: "Vergie Considine",
          tel: "351.951.8030 x0330",
          address: "8865 Conrad Mill",
          opening_hours: "08:00",
          description:
            "Quia omnis natus est praesentium dolores aliquid debitis omnis molestias.",
          image:
            "https://loremflickr.com/320/240/restaurant,food/?random=0.7508871784973614",
          viewCounts: 1,
          createdAt: "2020-02-28T14:38:32.000Z",
          updatedAt: "2020-03-09T06:09:15.000Z",
          CategoryId: 5
        }
      },
      {
        id: 63,
        text: "Et itaque rerum fugit.",
        UserId: 3,
        RestaurantId: 13,
        createdAt: "2020-02-28T14:38:32.000Z",
        updatedAt: "2020-02-28T14:38:32.000Z",
        Restaurant: {
          id: 13,
          name: "Mrs. Eileen Lockman",
          tel: "(597) 404-9974 x003",
          address: "383 Stroman Center",
          opening_hours: "08:00",
          description:
            "Vitae id incidunt animi qui sapiente perferendis iusto. Nemo placeat ut voluptas quae cupiditate eligendi. Expedita laborum vitae nulla quia ipsam. Et sunt a veniam culpa asperiores qui culpa. Odit reiciendis dolore reprehenderit est est voluptas ut rerum.  dddddd",
          image:
            "https://loremflickr.com/320/240/restaurant,food/?random=54.950245749491145",
          viewCounts: 7,
          createdAt: "2020-02-28T14:38:32.000Z",
          updatedAt: "2020-04-11T03:56:01.000Z",
          CategoryId: 2
        }
      },
      {
        id: 64,
        text: "Repellat magnam illo sit est dolor non eveniet harum.",
        UserId: 3,
        RestaurantId: 14,
        createdAt: "2020-02-28T14:38:32.000Z",
        updatedAt: "2020-02-28T14:38:32.000Z",
        Restaurant: {
          id: 14,
          name: "Boyd Abbott",
          tel: "172-684-6335",
          address: "50119 Nader Via",
          opening_hours: "08:00",
          description:
            "Aut aut enim sint sed. Vero qui voluptas voluptatem velit aut et numquam. Aut nesciunt sed aliquam. Non pariatur deserunt est. Quod illo dolorem sint et inventore culpa veritatis libero a.",
          image:
            "https://loremflickr.com/320/240/restaurant,food/?random=67.78299128798855",
          viewCounts: 7419,
          createdAt: "2020-02-28T14:38:32.000Z",
          updatedAt: "2020-04-08T09:14:01.000Z",
          CategoryId: 4
        }
      },
      {
        id: 68,
        text:
          "Ipsa facere repellendus impedit expedita dignissimos nisi asperiores totam ut.",
        UserId: 3,
        RestaurantId: 18,
        createdAt: "2020-02-28T14:38:32.000Z",
        updatedAt: "2020-02-28T14:38:32.000Z",
        Restaurant: {
          id: 18,
          name: "Ocie Deckow",
          tel: "837.390.8872 x4985",
          address: "74987 Hazel Alley",
          opening_hours: "08:00",
          description: "sit ut voluptas",
          image:
            "https://loremflickr.com/320/240/restaurant,food/?random=86.47034719848816",
          viewCounts: 1,
          createdAt: "2020-02-28T14:38:32.000Z",
          updatedAt: "2020-03-01T11:02:39.000Z",
          CategoryId: 3
        }
      },
      {
        id: 70,
        text: "Et sint consequatur.",
        UserId: 3,
        RestaurantId: 20,
        createdAt: "2020-02-28T14:38:32.000Z",
        updatedAt: "2020-02-28T14:38:32.000Z",
        Restaurant: {
          id: 20,
          name: "Ms. Stephanie Smith",
          tel: "1-574-132-5696 x54763",
          address: "1610 Piper View",
          opening_hours: "08:00",
          description:
            "Fugit inventore placeat ullam rerum quo ut. Dolorem ipsam tempore quisquam porro aspernatur dicta beatae. Magni aut in. Fugiat sit qui aut. testet",
          image:
            "https://loremflickr.com/320/240/restaurant,food/?random=38.787623335517175",
          viewCounts: 0,
          createdAt: "2020-02-28T14:38:32.000Z",
          updatedAt: "2020-03-25T14:41:17.000Z",
          CategoryId: 3
        }
      },
      {
        id: 74,
        text: "Reprehenderit sed beatae nihil.",
        UserId: 3,
        RestaurantId: 24,
        createdAt: "2020-02-28T14:38:32.000Z",
        updatedAt: "2020-02-28T14:38:32.000Z",
        Restaurant: {
          id: 24,
          name: "Jonathon Medhurst",
          tel: "078-927-0426",
          address: "081 Raheem Creek",
          opening_hours: "08:00",
          description:
            "Blanditiis sed aut mollitia nihil est saepe. Est repellendus vel iusto ex tempore. Cupiditate voluptas optio. Illo soluta qui.\n \rReprehenderit in sunt hic in culpa et. Et ab sequi id. Quia et itaque est distinctio ut ex doloremque dolor.\n \rDolorem eligendi animi dolor. Numquam corporis voluptatum. Et odit fugiat est.",
          image:
            "https://loremflickr.com/320/240/restaurant,food/?random=73.44969729408322",
          viewCounts: 0,
          createdAt: "2020-02-28T14:38:32.000Z",
          updatedAt: "2020-02-28T14:38:32.000Z",
          CategoryId: 4
        }
      },
      {
        id: 76,
        text: "Et cumque natus eum.",
        UserId: 3,
        RestaurantId: 26,
        createdAt: "2020-02-28T14:38:32.000Z",
        updatedAt: "2020-02-28T14:38:32.000Z",
        Restaurant: {
          id: 26,
          name: "Sarai Breitenberg",
          tel: "114-064-6388 x05451",
          address: "118 Cole Dale",
          opening_hours: "08:00",
          description:
            "Reiciendis et voluptatibus officiis magni enim quia pariatur ut. Fugit illum quia totam qui omnis facere minus. Dolores qui ullam magni enim repellat impedit hic ab aspernatur. Doloribus qui deleniti quas ipsum aut et. Odit perspiciatis cupiditate inventore omnis. Ut eum voluptatem facere quaerat aliquam doloremque perspiciatis id officiis.",
          image:
            "https://loremflickr.com/320/240/restaurant,food/?random=93.53330481196743",
          viewCounts: 3,
          createdAt: "2020-02-28T14:38:32.000Z",
          updatedAt: "2020-04-11T04:57:17.000Z",
          CategoryId: 4
        }
      },
      {
        id: 89,
        text: "Non beatae nesciunt sunt nostrum quia odio et minima optio.",
        UserId: 3,
        RestaurantId: 39,
        createdAt: "2020-02-28T14:38:32.000Z",
        updatedAt: "2020-02-28T14:38:32.000Z",
        Restaurant: {
          id: 39,
          name: "Christy Bauch",
          tel: "1-370-634-6490 x59473",
          address: "756 Dicki Ports",
          opening_hours: "08:00",
          description: "Earum aut delectus et voluptatibus ipsam deserunt ex.",
          image:
            "https://loremflickr.com/320/240/restaurant,food/?random=5.459083807432652",
          viewCounts: 0,
          createdAt: "2020-02-28T14:38:32.000Z",
          updatedAt: "2020-02-28T14:38:32.000Z",
          CategoryId: 2
        }
      },
      {
        id: 93,
        text:
          "Perferendis quam voluptatem rerum reprehenderit nihil perferendis aliquid.",
        UserId: 3,
        RestaurantId: 43,
        createdAt: "2020-02-28T14:38:32.000Z",
        updatedAt: "2020-02-28T14:38:32.000Z",
        Restaurant: {
          id: 43,
          name: "Mrs. Noemy Watsica",
          tel: "(252) 981-9430 x3227",
          address: "1218 Dariana Ports",
          opening_hours: "08:00",
          description:
            "Animi rerum suscipit iusto id autem et. Facilis id necessitatibus quia quo est perferendis quia velit. Ea dicta aspernatur assumenda alias autem repellat odit exercitationem. Rerum praesentium voluptatem corrupti soluta aut autem sapiente dolor.",
          image:
            "https://loremflickr.com/320/240/restaurant,food/?random=23.889387774329695",
          viewCounts: 0,
          createdAt: "2020-02-28T14:38:32.000Z",
          updatedAt: "2020-02-28T14:38:32.000Z",
          CategoryId: 5
        }
      },
      {
        id: 107,
        text: "Id eum nulla perferendis autem atque dolorum.",
        UserId: 3,
        RestaurantId: 7,
        createdAt: "2020-02-28T14:38:32.000Z",
        updatedAt: "2020-02-28T14:38:32.000Z",
        Restaurant: {
          id: 7,
          name: "Miss Letitia Will",
          tel: "(770) 750-6811 x99988",
          address: "8145 Laisha Keys",
          opening_hours: "08:00",
          description:
            "Aut earum molestiae et ducimus adipisci ut maxime.\r\nVeritatis labore illum et similique cumque qui qui officia omnis.\r\nQui laudantium amet enim natus.\r\nVoluptatem quia est nam ut esse et.",
          image: "https://i.imgur.com/50clDpn.jpg",
          viewCounts: 89,
          createdAt: "2020-02-28T14:38:32.000Z",
          updatedAt: "2020-05-19T06:28:30.000Z",
          CategoryId: 5
        }
      },
      {
        id: 114,
        text: "Fugit in suscipit voluptatibus veritatis.",
        UserId: 3,
        RestaurantId: 14,
        createdAt: "2020-02-28T14:38:32.000Z",
        updatedAt: "2020-02-28T14:38:32.000Z",
        Restaurant: {
          id: 14,
          name: "Boyd Abbott",
          tel: "172-684-6335",
          address: "50119 Nader Via",
          opening_hours: "08:00",
          description:
            "Aut aut enim sint sed. Vero qui voluptas voluptatem velit aut et numquam. Aut nesciunt sed aliquam. Non pariatur deserunt est. Quod illo dolorem sint et inventore culpa veritatis libero a.",
          image:
            "https://loremflickr.com/320/240/restaurant,food/?random=67.78299128798855",
          viewCounts: 7419,
          createdAt: "2020-02-28T14:38:32.000Z",
          updatedAt: "2020-04-08T09:14:01.000Z",
          CategoryId: 4
        }
      },
      {
        id: 116,
        text: "Sunt culpa ad sed ea.",
        UserId: 3,
        RestaurantId: 16,
        createdAt: "2020-02-28T14:38:32.000Z",
        updatedAt: "2020-02-28T14:38:32.000Z",
        Restaurant: {
          id: 16,
          name: "Aaliyah Lakin",
          tel: "1-235-923-9473 x43870",
          address: "1951 Jakubowski Villages",
          opening_hours: "08:00",
          description: "quidem",
          image:
            "https://loremflickr.com/320/240/restaurant,food/?random=91.06034163072859",
          viewCounts: 9,
          createdAt: "2020-02-28T14:38:32.000Z",
          updatedAt: "2020-04-11T04:16:08.000Z",
          CategoryId: 5
        }
      },
      {
        id: 118,
        text: "In quo temporibus qui aliquam libero.",
        UserId: 3,
        RestaurantId: 18,
        createdAt: "2020-02-28T14:38:32.000Z",
        updatedAt: "2020-02-28T14:38:32.000Z",
        Restaurant: {
          id: 18,
          name: "Ocie Deckow",
          tel: "837.390.8872 x4985",
          address: "74987 Hazel Alley",
          opening_hours: "08:00",
          description: "sit ut voluptas",
          image:
            "https://loremflickr.com/320/240/restaurant,food/?random=86.47034719848816",
          viewCounts: 1,
          createdAt: "2020-02-28T14:38:32.000Z",
          updatedAt: "2020-03-01T11:02:39.000Z",
          CategoryId: 3
        }
      },
      {
        id: 126,
        text: "Quos earum eum distinctio quaerat iste unde vitae eveniet.",
        UserId: 3,
        RestaurantId: 26,
        createdAt: "2020-02-28T14:38:32.000Z",
        updatedAt: "2020-02-28T14:38:32.000Z",
        Restaurant: {
          id: 26,
          name: "Sarai Breitenberg",
          tel: "114-064-6388 x05451",
          address: "118 Cole Dale",
          opening_hours: "08:00",
          description:
            "Reiciendis et voluptatibus officiis magni enim quia pariatur ut. Fugit illum quia totam qui omnis facere minus. Dolores qui ullam magni enim repellat impedit hic ab aspernatur. Doloribus qui deleniti quas ipsum aut et. Odit perspiciatis cupiditate inventore omnis. Ut eum voluptatem facere quaerat aliquam doloremque perspiciatis id officiis.",
          image:
            "https://loremflickr.com/320/240/restaurant,food/?random=93.53330481196743",
          viewCounts: 3,
          createdAt: "2020-02-28T14:38:32.000Z",
          updatedAt: "2020-04-11T04:57:17.000Z",
          CategoryId: 4
        }
      },
      {
        id: 131,
        text: "Odit cumque debitis voluptas soluta.",
        UserId: 3,
        RestaurantId: 31,
        createdAt: "2020-02-28T14:38:32.000Z",
        updatedAt: "2020-02-28T14:38:32.000Z",
        Restaurant: {
          id: 31,
          name: "Noe Raynor",
          tel: "1-595-633-3163 x052",
          address: "2075 Sharon Rapid",
          opening_hours: "08:00",
          description:
            "Quo voluptatum rerum temporibus enim nihil. Ea vitae odit quis ducimus doloremque veniam ut. Sequi debitis at et voluptas consectetur fugit qui. Vero voluptas quasi sed quam et sit. Atque id maxime voluptas. Dolorem voluptas facilis et odit optio sunt excepturi quaerat pariatur.",
          image:
            "https://loremflickr.com/320/240/restaurant,food/?random=43.066607162000324",
          viewCounts: 2,
          createdAt: "2020-02-28T14:38:32.000Z",
          updatedAt: "2020-04-10T14:30:59.000Z",
          CategoryId: 1
        }
      },
      {
        id: 132,
        text:
          "Adipisci ullam non aspernatur sapiente architecto dolorum accusamus molestiae aut.",
        UserId: 3,
        RestaurantId: 32,
        createdAt: "2020-02-28T14:38:32.000Z",
        updatedAt: "2020-02-28T14:38:32.000Z",
        Restaurant: {
          id: 32,
          name: "Rafael Schaden III",
          tel: "1-836-107-5530",
          address: "7262 Devyn Centers",
          opening_hours: "08:00",
          description:
            "Dicta perspiciatis aliquid voluptate tempore similique.",
          image:
            "https://loremflickr.com/320/240/restaurant,food/?random=2.1540435433775817",
          viewCounts: 0,
          createdAt: "2020-02-28T14:38:32.000Z",
          updatedAt: "2020-02-28T14:38:32.000Z",
          CategoryId: 1
        }
      },
      {
        id: 135,
        text: "Ut ipsum aut qui ut.",
        UserId: 3,
        RestaurantId: 35,
        createdAt: "2020-02-28T14:38:32.000Z",
        updatedAt: "2020-02-28T14:38:32.000Z",
        Restaurant: {
          id: 35,
          name: "Daphnee Lowe",
          tel: "548-757-2237",
          address: "232 Jennings Junctions",
          opening_hours: "08:00",
          description: "id dolores quis",
          image:
            "https://loremflickr.com/320/240/restaurant,food/?random=85.90083920238921",
          viewCounts: 0,
          createdAt: "2020-02-28T14:38:32.000Z",
          updatedAt: "2020-02-28T14:38:32.000Z",
          CategoryId: 4
        }
      },
      {
        id: 136,
        text: "Temporibus accusamus aliquid itaque labore.",
        UserId: 3,
        RestaurantId: 36,
        createdAt: "2020-02-28T14:38:32.000Z",
        updatedAt: "2020-02-28T14:38:32.000Z",
        Restaurant: {
          id: 36,
          name: "Telly Cole",
          tel: "1-857-419-5226",
          address: "307 Schoen Summit",
          opening_hours: "08:00",
          description:
            "Et dolores quis cum expedita voluptatem. Aspernatur et perspiciatis atque sit cupiditate sint voluptatum. Omnis magnam libero.",
          image:
            "https://loremflickr.com/320/240/restaurant,food/?random=75.63614517186328",
          viewCounts: 0,
          createdAt: "2020-02-28T14:38:32.000Z",
          updatedAt: "2020-02-28T14:38:32.000Z",
          CategoryId: 3
        }
      },
      {
        id: 138,
        text: "Sed dolores dicta reprehenderit provident provident labore.",
        UserId: 3,
        RestaurantId: 38,
        createdAt: "2020-02-28T14:38:32.000Z",
        updatedAt: "2020-02-28T14:38:32.000Z",
        Restaurant: {
          id: 38,
          name: "Will Simonis",
          tel: "607.753.9619 x395",
          address: "18639 Wilton Courts",
          opening_hours: "08:00",
          description: "laborum voluptas accusantium",
          image:
            "https://loremflickr.com/320/240/restaurant,food/?random=75.4278047434088",
          viewCounts: 1817,
          createdAt: "2020-02-28T14:38:32.000Z",
          updatedAt: "2020-03-02T17:05:56.000Z",
          CategoryId: 5
        }
      },
      {
        id: 142,
        text:
          "Officiis qui alias id possimus et iusto consequatur totam molestiae.",
        UserId: 3,
        RestaurantId: 42,
        createdAt: "2020-02-28T14:38:32.000Z",
        updatedAt: "2020-02-28T14:38:32.000Z",
        Restaurant: {
          id: 42,
          name: "Adrian Weimann",
          tel: "(102) 131-9224 x2147",
          address: "04294 Nils Track",
          opening_hours: "08:00",
          description:
            "Et dolores eos sed aut doloribus velit autem quae. Debitis recusandae occaecati ut rerum. Esse dolorum dolorum velit nemo. Culpa mollitia non maxime aspernatur neque aut voluptates architecto.\n \rAnimi veniam nesciunt ut est assumenda voluptatem omnis eligendi. Nam incidunt sint. Reprehenderit et eveniet est laborum ut. Et consequuntur quod ut.\n \rSequi id natus voluptatem repudiandae doloremque pariatur quaerat sit. Quibusdam ipsa voluptatem consequatur at. Illo ullam illum. Enim et cum nulla. Illum debitis et.",
          image:
            "https://loremflickr.com/320/240/restaurant,food/?random=57.71296646754862",
          viewCounts: 2,
          createdAt: "2020-02-28T14:38:32.000Z",
          updatedAt: "2020-03-22T08:10:15.000Z",
          CategoryId: 4
        }
      },
      {
        id: 146,
        text: "Iste dolor mollitia qui a ex error soluta.",
        UserId: 3,
        RestaurantId: 46,
        createdAt: "2020-02-28T14:38:32.000Z",
        updatedAt: "2020-02-28T14:38:32.000Z",
        Restaurant: {
          id: 46,
          name: "Mr. Price Heathcote",
          tel: "1-234-170-6861",
          address: "178 Collins Mission",
          opening_hours: "08:00",
          description: "Unde maiores error ex.",
          image:
            "https://loremflickr.com/320/240/restaurant,food/?random=38.75335489939356",
          viewCounts: 20,
          createdAt: "2020-02-28T14:38:32.000Z",
          updatedAt: "2020-03-24T11:04:19.000Z",
          CategoryId: 4
        }
      }
    ],
    FavoritedRestaurants: [
      {
        id: 13,
        name: "Mrs. Eileen Lockman",
        tel: "(597) 404-9974 x003",
        address: "383 Stroman Center",
        opening_hours: "08:00",
        description:
          "Vitae id incidunt animi qui sapiente perferendis iusto. Nemo placeat ut voluptas quae cupiditate eligendi. Expedita laborum vitae nulla quia ipsam. Et sunt a veniam culpa asperiores qui culpa. Odit reiciendis dolore reprehenderit est est voluptas ut rerum.  dddddd",
        image:
          "https://loremflickr.com/320/240/restaurant,food/?random=54.950245749491145",
        viewCounts: 7,
        createdAt: "2020-02-28T14:38:32.000Z",
        updatedAt: "2020-04-11T03:56:01.000Z",
        CategoryId: 2,
        Favorite: {
          UserId: 3,
          RestaurantId: 13,
          createdAt: "2020-03-30T01:34:36.000Z",
          updatedAt: "2020-03-30T01:34:36.000Z"
        }
      }
    ],
    Followers: [
      {
        id: 242,
        name: "abc",
        email: "abc@abc",
        password:
          "$2a$10$seMk2.DnlqD708UVY3SAtuFpQcGMa9TwwR0BuHzeennUFxIBk1LnC",
        isAdmin: false,
        image: null,
        createdAt: "2020-03-26T08:03:08.000Z",
        updatedAt: "2020-03-26T08:03:08.000Z",
        Followship: {
          followerId: 242,
          followingId: 3,
          createdAt: "2020-03-30T01:31:47.000Z",
          updatedAt: "2020-03-30T01:31:47.000Z"
        }
      }
    ],
    Followings: [
      {
        id: 102,
        name: "asd@asd.asd",
        email: "asd@asd.asd",
        password:
          "$2a$10$r9jgmPQGI2uN59XwkuTiX.qRORpqYDoMg8e36WJ.bw1JexPvpXVp.",
        isAdmin: false,
        image: "https://i.imgur.com/yJTFCDh.jpg",
        createdAt: "2020-03-09T06:15:49.000Z",
        updatedAt: "2020-03-09T06:16:09.000Z",
        Followship: {
          followerId: 3,
          followingId: 102,
          createdAt: "2020-03-30T03:25:48.000Z",
          updatedAt: "2020-03-30T03:25:48.000Z"
        }
      },
      {
        id: 72,
        name: "mohammad akhbarati",
        email: "makhbarati@gmail.com",
        password:
          "$2a$10$ljaWKqtQwgLA5BdTEhBTHeJK/Ku4ow3IHM4S5OJYmr7.anBAIl7NW",
        isAdmin: true,
        image: null,
        createdAt: "2020-02-29T23:24:32.000Z",
        updatedAt: "2020-04-21T10:01:23.000Z",
        Followship: {
          followerId: 3,
          followingId: 72,
          createdAt: "2020-03-30T04:25:20.000Z",
          updatedAt: "2020-03-30T04:25:20.000Z"
        }
      },
      {
        id: 62,
        name: "AC",
        email: "ac@ac.com",
        password:
          "$2a$10$yB01LxQAujWjRQ0WaprYV.t5SDx6kool5Cmrt0F7TRSXGRk.W8z1m",
        isAdmin: true,
        image: null,
        createdAt: "2020-02-29T15:41:09.000Z",
        updatedAt: "2020-04-21T10:00:59.000Z",
        Followship: {
          followerId: 3,
          followingId: 62,
          createdAt: "2020-04-04T04:53:41.000Z",
          updatedAt: "2020-04-04T04:53:41.000Z"
        }
      }
    ]
  },
  isFollowed: false
};
export default {
  components: {
    UserEditCard
  },
  data() {
    return {
      profile: {}
    };
  },
  methods: {
    handleAfterSubmit(formData) {
      console.log("透過 API 將表單資料送到伺服器");
      for (let [name, value] of formData.entries()) {
        console.log(name + ": " + value);
      }
    },
    fetchUser(userId) {
      console.log("userId", userId);
      this.profile = dummyData.profile;
    }
  },
  created() {
    const { id } = this.$route.params;
    this.fetchUser(id);
  }
};
</script>