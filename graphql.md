## # GraphQL

<br>

### # GraphQL 이란?

<br>

- GraphQL은 facebook에서 개발한 Graph Query Language로 API를 위한 쿼리 언어이며 타입 시스템을 사용하여 쿼리를 실행하는 서버사이드 런타임이다. 핵심적으로 GraphQL은 클라이언트가 API에서 필요한 데이터를 정확히 지정할 수있는 선언적(decalarative) 데이터 패칭을 지원한다. 고정 데이터 구조를 반환하는 여러 엔드 포인트 대신 GraphQL 서버는 단일 엔드 포인트만 노출하고 클라이언트가 요청한 데이터로 정확하게 응답한다.

  ![graphqlvsrestapi](https://user-images.githubusercontent.com/85284246/189499801-376ee809-c5e5-4b92-857e-5cc0a59a19ed.png)

<br>

### # REST의 단점

<br>

- 오버패칭(overfetching) : 필요하지 않은 데이터를 너무 많이 받아온다.

- 언더패칭(underfetching) : 필요한 데이터를 수집하기 위해 여러 번의 요청을 수행해야 하는 상황이 발생한다.

- 엔드포인트 관리 문제 : 클라이언트에 변경사항이 발생하면 대개 엔드포인트를 새로 만들어야 하는데, 이렇게 되면 엔드포인트 개수가 몇 배로 빠르게 늘어난다.

<br>

### # GraphQL vs REST

<br>

- 형태 정의 및 데이터 요청 방식 : 자원에 대한 접근을 할 때 REST API는 형태를 정의하고 요청방법이 연결되어 있지만 GraphQL 상에서는 분리되어 있다.

- 자원의 크기와 형태 결정 주체 : REST 상에서는 서버쪽에서 결정하지만, GraphQL은 자원에 대한 정보만 정의하고 필요한 요소들은 Client 요청 시 결정한다.

- 작업의 유형 : REST 상에서는 url과 method가 결정하지만 GraphQL은 Schema가 Resource를 나타내고 Query, Mutation 타입이 작업의 유형을 나타낸다.

- 요청 횟수 : REST는 여러 자원에 접근할 때 여러 번의 요청이 필요하지만 GraphQL에서는 한번의 요청에서 여러 Resource에 접근할 수 있다.

- 작업 처리 방식 : REST에서 각 요청은 해당 엔드포인트에 정의된 핸들링 함수를 호출하여 작업을 처리하지만, GraphQL에서는 요청 받은 각 필드에 대한 resolver를 호출하여 작업을 처리한다.

<br><br>

## # 그래프(Graph)

<br>

- 그래프는 보통 노드, 정점이라고 부르는 추상 객체로 이루어져있다. 두 노드 사이의 선은 edge(엣지)라고 부르며 우리는 특정한 순서에 의해 엣지를 따라 그래프를 재귀적으로 탐색할 수 있다.

  ![randomGraph](https://user-images.githubusercontent.com/85284246/189503072-8c4c5d8a-f4a9-4099-9f70-cd978c9b4015.png)

<br>

### # 그래프(Graph)와 트리(Tree)

<br>

- 그래프는 어떤 조건이 부여됨에 따라 다른 자료 구조로 변할 수가 있다. 그래프 순회는 마지막 엣지가 첫 엣지인 자료의 집합인데, 이때 그래프에 순회가 없다면 이를 순환 지시 그래프라고 부르며 방향 그래프는 일종의 순환 지시 그래프이다. 그리고 이를 트리라고 부르기도 한다. 간단하게 생각하면 그래프에 루트 노드가 있다면 트리 그래프이다.

  ![graphVersusTree](https://user-images.githubusercontent.com/85284246/189503202-4dcb293c-410e-4925-a444-d2abe1acd893.jpeg)

<br><br>

## # GraphQL 쿼리어

<br>

- REST API를 사용할 때에는 특정 엔드포인트를 통하여 데이터를 불러오게 된다. 각 엔드포인트는 반환할 정보에 대하여 명확하게 정의한 구조를 가진다. 즉, 클라이언트의 데이터 요구 사항은 클라이언트가 접근하는 URL 상에서 반영된다.

  GraphQL이 취하는 접근 방식은 상당히 다르다. GraphQL은 고정된 형식의 데이터 구조를 반환하는 엔드포인트 여러 가지를 가지는 것이 아니라, 일반적으로 단 하나의 엔드포인트만을 노출시킨다. 반환되는 데이터의 구조가 고정적이지 않고 오히려 아주 유연하기 때문에 가능한 작업이다. 따라서 클라이언트 측에서 필요한 데이터를 결정할 수 있다.

  즉, 필요한 데이터가 무엇인지 서버에 알려주기 위하여 클라이언트가 보다 많은 정보를 보내야 한다는 뜻이다. 여기서 이 정보를 쿼리라고 부른다. 아래 이미지는 쿼리의 구조이다.

  ![query](https://user-images.githubusercontent.com/85284246/189499800-d784d0d5-4dd4-487b-9697-92134c477d9b.png)

<br>

### # 쿼리(Query)

<br>

- 쿼리(query)는 GraphQL 타입으로 루트 타입이라고 하는데 타입 하나가 하나의 작업을 수행한다. 쿼리는 데이터를 조회할 때 사용된다. 쿼리 안에는 GraphQL 서버에서 받고 싶은 데이터를 써 넣으면 된다. 쿼리를 보낼 때는 요청 데이터를 중괄호로 감싸 필드로 적어 넣는다. 여기서 필드는 서버에서 받아오는 JSON 응답 데이터의 필드와 일치한다. 또한 이 중괄호로 묶인 블록을 셀렉션 세트라고 하며 셀렉션 세트는 서로 중첩시킬 수 있다.

  ```js
  // request
  query liftsAndTrails {
    liftCount(status: OPEN)
    allLifts {
      name
      status
    }
    allTrails {
      name
      difficulty
    }
  }
  ```

- 위와 같이 정상적인 쿼리를 보내면 아래와 같이 data 키가 들어있는 JSON 문서가 응답으로 돌아오고 비정상적인 쿼리에는 응답으로 error 키가 들어있는 JSON 문서가 돌아온다. 이 키 값으로는 에러에 대한 세부적인 내용이 들어간다. data와 error 키가 응답 객체에 동시에 포함된 경우도 있다.

  ```json
  // response
  {
    "data": {
      "liftCount": 6,
      "allLifts": [
        {
          "name": "Astra Express",
          "status": "OPEN"
        },
        ...
      ],
      "allTrails": [
        {
          "name": "Blue Bird",
          "difficulty": "intermediate"
        },
        ...
      ]
    }
  }
  ```

<br>

### # 별칭(Alias)

<br>

- 응답 객체의 필드명을 다르게 받고 싶다면, 쿼리 안의 필드명에 별칭(Alias)을 부여하면 된다. `별칭 : 필드 이름` 의 형태로 별칭을 부여할 수 있다.

  ```js
  // request
  // open, charilifts, liftname, skiSlopes 등 별칭 부여
  query liftsAndTrails {
    open : liftCount(status: OPEN)
    charilifts: allLifts {
      liftname : name
      status
    }
      skiSlopes: allTrails {
      name
      difficulty
    }
  }
  ```

  ```json
  // response
  // 부여한 별칭으로 필드 이름이 변한 것을 볼 수 있다.
  {
    "data": {
      "open": 6,
      "charilifts": [
        {
          "liftname": "Astra Express",
          "status": "CLOSED"
        }
        ...
      ],
      "skiSlopes": [
        {
          "name": "Blue Bird",
          "difficulty": "intermediate"
        }
        ...
      ]
    }
  }
  ```

<br>

### # 프래그먼트(Fragement)

<br>

- 프래그먼트는 셀렉션 세트의 일종이며 여러 번 재사용할 수 있다. `fragment` 식별자를 사용하여 만들고 특정 타입에 대한 셀렉션 세트이므로 어떤 타입에 대한 프래그먼트인지 정의에 꼭 명시해야 한다.

  ```js
  // request
  // 프래그먼트 활용 전 : name, status, capacity, night, elevationGain가 중복된다.
  query {
    Lift(id: "jazz-cat"){
      name
      status
      capacity
      night
      elevationGain
      trailAccess {
        name
        difficulty
      }
    }
    Trail(id: "river-run"){
      name
      difficulty
      accessedByLifts {
        name
        status
        capacity
        night
        elevationGain
      }
    }
  }

  // 프래그먼트 활용 후 : js의 spread 문법과 비슷하게 사용하여 중복 필드를 줄일 수 있다. 프래그먼트 활용 전과 응답 결과는 동일하다.
  query {
    Lift(id: "jazz-cat"){
        ...liftInfo
      trailAccess {
        name
        difficulty
      }
    }
    Trail(id: "river-run"){
      name
      difficulty
      accessedByLifts {
        ...liftInfo
      }
    }
  }

  fragment liftInfo on Lift {
    name
    status
    capacity
    night
    elevationGain
  }
  ```

- 셀렉션 세트 안에 프래그먼트를 다른 필드와 함께 쓸 수도 있다.

  ```js
  query {
    Lift(id: "jazz-cat"){
      ...liftInfo
      trailAccess{
        ...trailInfo
      }
    }
    Trail(id: "river-run"){
      ...trailInfo
      groomed
      trees
      night
    }
  }

  fragment trailInfo on Trail {
    name
    difficulty
    accessedByLifts {
      ...liftInfo
    }
  }

  fragment liftInfo on Lift {
    name
    status
    capacity
    night
    elevationGain
  }
  ```

<br>

### # 유니온(Union)타입과 인라인 프래그먼트(Inline Fragment)

<br>

- 타입 여러 개를 한 번의 리스트에 담아 반환하고 싶다면 유니온 타입을 만들면 된다. 유니온 타입은 두 가지 타입을 하나로 묶는 것이다. 유니온 타입에서 각각의 객체가 어떤 필드를 반환할 지 정할 때 인라인 프래그먼트를 사용한다. 인라인 프래그먼트는 이름이 없으며 쿼리 안에서 특정 타입을 바로 셀렉션 세트에 넣어버린다.

  ```js
  type StudyGroup {
      name: String!
      subject: String!
      students: Int!
  }

  type Workout {
      name: String!
      reps: Int!
  }

  union AgendaItem = Workout | StudyGroup

  type Query {
    agenda: [AgendaItem!]!
  }

  // AgendaItem이 Workout일때와 StudyGroup일때 특정 필드만 선택되도록 만들 수 있다.
  {
    agenda {
      ...on Workout {
        name
        reps
      }
      ...on StudyGroup {
        name
        subject
        students
      }
    }
  }
  ```

- 이름 붙은 프래그먼트를 사용해 유니온 타입 쿼리를 작성할 수도 있다.

  ```js
  query today{
    agenda {
      ...workout
      ...study
    }
  }

  fragment workout on Workout {
    name
    reps
  }

  fragment study on StudyGroup {
    name
    subject
    students
  }
  ```

<br>

### # 인터페이스(Interface)타입과 프래그먼트(Fragement)

<br>

- 인터페이스는 필드 하나로 객체 타입을 여러 개 반환할 때 사용한다. 또한 유사한 객체 타입을 만들 때 구현해야 하는 필드 리스트를 모아둘 수 있으며 인터페이스에 정의된 필드는 필수로 구현해야 하고 몇 가지 고유한 필드도 추가로 넣을 수 있다. 인터페이스 타입 사용 시 아래와 같이 프래그먼트를 사용하면 특정 객체 타입이 반환될 때, 필드가 더 들어갈 수 있게 인터페이스 관련 쿼리를 작성할 수 있다.

  ```js
  interface ScheduleItem {
    name: String!
    start: Int
    end: Int
  }

  type StudyGroup implements ScheduleItem {
    name: String!
    start: Int
    end: Int
    subject: String!
    students: Int!
  }

  type Workout implements ScheduleItem {
    name: String!
    start: Int
    end: Int
    reps: Int!
  }

  type Query {
    agenda: [ScheduleItem!]!
  }

  // 프래그먼트를 사용하여 ScheduleItem이 Workout일 때 reps 필드를 추가로 요청할 수 있다.
  query schedule {
    agenda {
      name
      start
      end
      ...on Workout {
        reps
      }
    }
  }
  ```

<br>

### # 뮤테이션(Mutation)

<br>

- 데이터의 추가/수정/삭제를 위해서는 뮤테이션(mutation)을 사용할 수 있다. 쿼리를 작성하는 방법과 비슷하다. 쿼리와 마찬가지로 스키마에는 뮤테이션 타입에서 사용할 수 있는 필드를 정의해두며 뮤테이션 후에는 뮤테이션으로 변경 된 데이터를 응답받는다.

  ```js
  // request
  // 새로운 음악 데이터를 추가될 것임을 예상할 수 있다.
  mutation createSong {
    addSong (title: "No Scrubs", numberOne: true, performerName: "TLC") {
      id
      title
      numberOne
    }
  }
  ```

  ```json
  // response
  {
    "data": {
      "addSong": {
        "id": "5aca534f4bb1de07cb6d73ae",
        "title": "No Scrubs",
        "numberOne": true
      }
    }
  }
  ```

- 뮤테이션으로 기존 데이터 변경도 가능하다.

  ```js
  // request
  // 1. 전체 Lifts 데이터 중 status가 CLOSED인 데이터를 조회하는 쿼리이다.
  query closedLifts {
  	allLifts(status: CLOSED) {
      name
      status
    }
  }

  // 2. id가 astra-express인 필드의 status를 OPEN에서 CLOSED로 바꾼다.
  mutation closeLift {
    setLiftStatus(id: "astra-express", status: CLOSED){
      name
      status
    }
  }
  ```

  ```json
  // 3. response : 뮤테이션 closeLift로 데이터를 수정한 뒤 쿼리 closedLifts에 대한 응답
  // astra-express가 CLOSE 상태로 추가된 것을 확인할 수 있다.
  {
    "data": {
      "allLifts": [
        {
          "id": "astra-express",
          "name": "Astra Express",
          "status": "CLOSED"
        },
        {
          "id": "summit",
          "name": "Summit",
          "status": "CLOSED"
        },
        {
          "id": "western-states",
          "name": "Western States",
          "status": "CLOSED"
        }
      ]
    }
  }
  ```

<br>

### # 변수(Variable)

<br>

- 위와 같이 새 문자열 값을 뮤테이션의 인자로 넘겨 데이터 변경 작업을 할 수 있는데 변수를 사용해도 같은 결과를 얻을 수 있다. 쿼리에 있는 정적 값을 변수로 대체하여 계속해서 바뀌는 동적인 값을 넣을 수도 있다. 쿼리 변수는 객체 형태로 전달되어야 한다.

  ```js
  // request
  // 새로운 음악 데이터를 추가될 것임을 예상할 수 있다.
  mutation createSong($title: String!, $numberOne: Int, $performerName: String!) {
    addSong (title: $title, numberOne: $numberOne, performerName: $performerName) {
      id
      title
      numberOne
    }
  }
  ```

  ```json
  // response
  {
    "data": {
      "addSong": {
        "id": "5aca534f4bb1de07cb6d73ae",
        "title": "No Scrubs",
        "numberOne": true
      }
    }
  }
  ```

<br>

### # 서브스크립션(Subscription)

<br>

- 서브스크립션을 하면 GraphQL API를 사용해 실시간 데이터 변경 내용을 받을 수 있다. 즉 구독의 개념이다. 페이스북의 실시간 좋아요는 데이터 서브스크립션 기능을 실제 제품에 적용한 사례이다. 뮤테이션과 쿼리처럼 서브스크립션도 루트 타입이 있다. 서브스크립션 요청 시 즉시 데이터를 반환하는 것이 아닌 서브스크립션 요청이 서버로 전송되면 받는 쪽에서 데이터의 변경 사항 여부를 듣기 시작하며 서브스크립션 대상 데이터의 변경 내용을 포착하면 서브스크립션 요청에 대한 응답을 받을 수 있다. 즉 뮤테이션을 구독하고 뮤테이션이 실행되면 구독하고 있던 서브스크립션이 실행된다고 보면 된다. 또한 쿼리와 뮤테이션과는 달리 서브스크립션은 일회성으로 끝나지 않고 계속 열려있게 된다.

  ```js
  // request
  // 1. 뮤테이션 실행
  mutation closeLift {
    setLiftStatus(id: "astra-express", status: HOLD){
      name
      status
    }
  }

  // 2. 서브스크립션 실행
  subscription {
    liftStatusChange {
      name
      capacity
      status
    }
  }
  ```

  ```json
  // response
  // 서브스크립션의 응답 결과로 뮤테이션으로 수정 된 결과 값을 받아볼 수 있다.
  {
    "data": {
      "liftStatusChange": {
        "name": "Astra Express",
        "capacity": 3,
        "status": "HOLD"
      }
    }
  }
  ```

<br>

### # 인트로스펙션(Instrospection)

<br>

- 인스트로펙션(Instrospection)을 사용하면 스키마의 세부 사항에 관한 쿼리를 작성할 수 있다. 어떤 데이터를 반환받을 수 있는 지 조사할 수 있으며 루트 타입, 커스텀 타입, 스칼라 타입까지 확인할 수 있다.

  ```js
  // request
  query {
    __schema {
      types {
        name
        description
      }
    }
  }
  ```

  ```json
  // response
  // API에서 사용할 수 있는 타입을 모두 볼 수 있다.
  {
    "data": {
      "__schema": {
        "types": [
          {
            "name": "Lift",
            "description": "A `Lift` is a chairlift, gondola, tram, funicular, pulley, rope tow, or other means of ascending a mountain."
          },
          {
            "name": "ID",
            "description": "The `ID` scalar type represents a unique identifier, often used to refetch an object or as key for a cache. The ID type appears in a JSON response as a String; however, it is not intended to be human-readable. When expected as an input type, any string (such as `\"4\"`) or integer (such as `4`) input value will be accepted as an ID."
          },
          ...
        ]
      }
    }
  }
  ```

- 특정 타입에 관한 세부 사항만 보고 싶다면 `__type` 쿼리에 타입명을 인자로 넘기면 된다.

  ```js
  // request
  query liftDetails {
    __type(name: "Lift") {
      name
      fields {
        name
        description
        type {
          name
        }
      }
    }
  }
  ```

  ```json
  // response
  // Lift 타입 관련 쿼리를 작성할 때 넣을 수 있는 필드 정보를 받아볼 수 있다.
  {
    "data": {
      "__type": {
        "name": "Lift",
        "fields": [
          {
            "name": "id",
            "description": "The unique identifier for a `Lift` (id: \"panorama\")",
            "type": {
              "name": null
            }
          },
          {
            "name": "name",
            "description": "The name of a `Lift`",
            "type": {
              "name": null
            }
          }
          ...
        ]
      }
    }
  }
  ```

- GraphQL API를 처음 사용할 때는 루트 타입에서 사용할 수 있는 필드가 무엇이 있는지 알아 보아야 한다. 아래와 같이 클라이언트에서 인트로스펙션 기능을 사용하면 현재 API 스키마의 동작 방식을 알아볼 수 있다.

  ```js
  // request
  query {
    __schema{
      queryType{
        ...typeFields
      }
      mutationType{
        ...typeFields
      }
      subscriptionType{
        ...typeFields
      }
    }
  }

  fragment typeFields on __Type {
    name
    fields {
      name
    }
  }
  ```

  ```json
  // response
  {
    "data": {
      "__schema": {
        "queryType": {
          "name": "Query",
          "fields": [
            {
              "name": "allLifts"
            },
            {
              "name": "allTrails"
            },
            {
              "name": "Lift"
            },
            {
              "name": "Trail"
            },
            {
              "name": "liftCount"
            },
            {
              "name": "trailCount"
            },
            {
              "name": "search"
            }
          ]
        },
        "mutationType": {
          "name": "Mutation",
          "fields": [
            {
              "name": "setLiftStatus"
            },
            {
              "name": "setTrailStatus"
            }
          ]
        },
        "subscriptionType": {
          "name": "Subscription",
          "fields": [
            {
              "name": "liftStatusChange"
            },
            {
              "name": "trailStatusChange"
            }
          ]
        }
      }
    }
  }
  ```

<br>

### # 추상 구문 트리(Abstract syntax tree)

<br>

- 쿼리 문서는 문자열로 이루어져 있다. GraphQL API로 쿼리를 보낼 때, 문자열은 추상 구문 트리로 파싱되어 명령 실행 전에 유효성 검사를 거친다. 추상 구문 트리는 계층 계층 구조를 지닌 객체로 쿼리를 표현하는데 사용하며 쿼리에 관한 부가 정보 필드가 중첩된 구조로 들어간다. 쿼리의 요청과 응답은 아래와 같은 과정으로 진행된다.

  1. 쿼리 요청이 발생하면 쿼리 문자열을 더 작은 여러 개의 조각으로 쪼개어 분석하는 어휘 분석 작업 실행

  2. 어휘 분석 작업이 끝난 뒤 추상 구문 트리로 가공 됨

  3. GraphQL은 가공 된 추상 구문 트리를 횡단하며 GraphQL 언어와 현재 스키마를 비교해 유효성 검사를 실시

  4. 구문에 오류가 없고 요청에서 요구한대로 스키마에 필드와 타입이 다 들어 있다면 작업이 정상적으로 실행

  5. 만약 구문에 오류가 있다면 특정 에러를 반환

<br>

## # 스키마 설계하기

<br>

- REST가 엔드포인트의 집합이라면 GraphQL은 타입 집합이다. API에서 반환할 데이터 타입을 정의하는데 이러한 데이터 타입의 집합을 스키마라고 한다. 또한 GraphQL은 스키마 정의를 위해 SDL(Schema Definition Language)를 지원한다. 또한 GraphQL은 스키마를 바탕으로 데이터가 매치되게 할 수 있고 데이터를 바탕으로 스키마가 생성되게 할 수 있다. 전자인 스키마를 바탕으로 데이터가 매치되게 하는 방법은 스키마 퍼스트 방식으로 스키마 퍼스트는 디자인 방법론의 일종이다. 스키마 퍼스트를 사용하면 백엔드 팀은 스키마를 보고 어떤 데이터를 저장하고 전달해야 하는지 이해할 수 있고 프론트엔드 팀은 사용자 인터페이스 작업을 할 때 필요한 데이터를 정의할 수 있다.

<br>

### # 타입 정의하기

<br>

- 객체 타입과 스칼라 타입 : 객체 타입은 해당 타입의 특성을 표현하는 필드들로 구성된다. 내장 스칼라 타입은 Int, Float, String, Boolean, ID가 있다. 또한 내장 스칼라 타입 외에도 커스텀 스칼라 타입을 직접 만들어 사용할 수 있다. npm 패키지 중 `graphql-custom-type` 은 자주 사용할 법한 커스텀 스칼라 타입을 모아둔 패키지도 있다.

  ```js
  scalar DataTime

  type Photo {
    id: ID!
    name: String!
    url: String!
    description: String
    created: DataTime!
  }
  ```

<br>

- 리스트 타입 : GraphQL 스키마 필드에서는 GraphQL 타입이 담긴 리스트 반환도 가능하다. 리스트는 GraphQL 타입을 대괄호로 감싸서 만든다. 또한 유니온이나 인터페이스 타입을 사용하면 리스트에 여러 개의 타입을 한 번에 담을 수도 있다.

  > #### # 리스트 !(non-nullable) 적용 규칙
  >
  > 1.  [Int] : 리스트 안에 담긴 정수 값은 null이 될 수 있다.
  > 2.  [Int!] : 리스트 안에 담긴 정수 값은 null이 될 수 없다.
  > 3.  [Int]! : 리스트 안에 담긴 정수 값은 null이 될 수 있으나, 리스트 자체는 null이 될 수 없다.
  > 4.  [Int!]! : 리스트 안에 담긴 정수 값은 null이 될 수 없고, 리스트 자체도 null이 될 수 없다.

<br>

- 이넘(enum) 타입 : 이넘 타입은 스칼라 타입에 속하며 필드에서 반환하는 문자열 값을 세트로 미리 지정해 둘 수 있다. 미리 정의해 둔 세트에 속하는 값만 필드에서 반환하도록 만들고 싶다면 이넘 타입을 사용하면 된다.

  ```js
  // 이넘 타입 사용
  // Photo의 category 필드는 Photocategory 내부에 정의 된 값들 중 하나를 반환한다.
  enum Photocategory {
    SELFIE
    PORTRAIT
    ACTION
    LANDSCAPE
    GRAPHIC
  }

  type Photo {
    id: ID!
    name: String!
    url: String!
    description: String
    created: DataTime!
    category: Photocategory!
  }
  ```

<br>

- 유니온(Union) 타입 : 유니온 타입은 한 필드 안에 타입을 여러 개 넣을 때 사용한다. 인터페이스와 매우 유사하지만, 타입 간에 공통 필드를 특정하지 않는다. 일정 앱을 예시로 일정에는 여러 종류의 이벤트가 들어가며 이벤트마다 데이터 필드가 달라질 수 있다.

  ```js
  // 스케쥴 쿼리
  // 유니언 타입 사용
  query schedule {
    agenda {
      ...on Workout {
        name
        reps
      }
      ...on StudyGroup {
        name
        subject
        students
      }
    }
  }

  union AgendaItem = StudyGroup | Workout

  type StudyGroup {
    name: String!
    subject: String!
    students: [User!]!
  }

  type Workout {
    name: String!
    reps: Int!
  }

  type Query {
    agenda : [AgendaItem!]!
  }
  ```

<br>

- 인터페이스(Interface) 타입 : 인터페이스 타입도 유니온 타입과 마찬가지로 한 필드 안에 타입을 여러 개 넣을 때 사용한다. 인터페이스 타입을 활용하면 특정 필드가 무조건 특정 타입에 포함되도록 만들 수 있다. 아래 예시의 경우 AgendaItem이라는 추상 타입을 만들고 확장하여 다른 타입을 만든다. 이렇게 만들게 되면 AgendaItem을 기반으로 만들어진 StudyGroup과 Workout 타입은 name, start, end가 필수적으로 들어가야 한다.

  ```js
  scalar DateTime

  interface AgendaItem {
    name: String!
    start: DateTime!
    end: DateTime!
  }

  type StudyGroup implements AgendaItem {
    name: String!
    start: DateTime!
    end: DateTime!
    participants: [User!]!
    topic: String!
  }

  type Workout implements AgendaItem {
    name: String!
    start: DateTime!
    end: DateTime!
    reps: Int!
  }

  type Query {
    agenda: [AgendaItem!]!
  }

  query schedule {
    agenda {
      name
      start
      end
      ...on Workout {
        reps
      }
    }
  }
  ```

- 일반적으로 객체에 따라 필드가 완전히 달라져야 한다면 유니언 타입을 쓰는 편이 좋고 특정 필드가 반드시 들어가야 한다면 인터페이스 타입이 적절하다.

<br>

### # 커스텀 객체 타입의 연결 관계

<br>

- 일대일 연결 : 각각의 객체 타입을 노드라고 가정했을 때 이 객체 타입의 연결이 필요한 경우 엣지가 필요하다. Photo와 User는 단방향 관계이며 두 노드를 이어주는 엣지는 postedBy가 된다.

  ```js
  // 스키마
  // Photo(Node) -> User(Node), 중간 화살표가 Edge이며 postedBy가 된다.
  type User {
    githubLogin : ID!
    name: String
    avatar : String
  }

  type Photo {
    id: ID!
    name: String!
    url: String!
    description: String
    created: DateTime!
    category: PhotoCategory!
    postedBy: User!
  }
  ```

<br>

- 일대다 연결 : GraphQL 서비스는 최대한 방향성이 없도록 유지하는 편이 좋다. 방향이 없다면 아무 노드에서 그래프 횡단을 시작할 수 있으므로, 클라이언트 쪽에서 쿼리를 최대한 자유롭게 만들 수 있기 때문이다. 일대다 관계는 어떤 객체(부모)의 필드에서 다른 객체 리스트(자식)를 반환하는 필드를 보유하고 있을 때 나타나는 관계이다. 아래 예시의 경우 한 유저는 여러 개의 사진을 게시할 수 있으므로 User -> 다수의 Photo의 관계가 되고 일대다 관계이다.

  ```js
  // 스키마
  // User(Node) -> 다수의 Photo(Node), 중간 화살표가 Edge이며 postedPhotos가 된다.
  type User {
    githubLogin : ID!
    name: String
    avatar : String
    postedPhotos: [Photo!]!
  }

  type Photo {
    id: ID!
    name: String!
    url: String!
    description: String
    created: DateTime!
    category: PhotoCategory!
    postedBy: User!
  }
  ```

<br>

- 다대다 연결 : 가끔 노드 리스트를 다른 노드 리스트와 연결지어야 할 때도 있다. 다대다 연결 관계를 만드려면 노드 양쪽 모두에 리스트 타입 필드를 추가하면 된다. 사진 앱을 예시로 한 장의 사진에는 여러 명의 사용자가 태그 될 수 있고, 한 명의 사용자가 여러 장의 사진에 태그될 수 있다.

  ```js
  // 스키마
  // User는 사진 여러 장에 태그 될 수 있다.
  // Photo에서는 사진 한 장에 여러 명을 태그할 수 있다.
  type User {
    ...
    inPhotos: [Photo!]!
  }

  type Photo {
    ...
    taggedUsers: [User!]!
  }
  ```

<br>

- 다대다 연결을 만들 경우 관계 자체에 대한 정보를 담고 싶을 때도 있다. 이럴 때 통과 타입을 사용할 수 있다. 통과 타입은 공식 스펙은 아니다. 아래 예제에서는 friends 필드를 User 타입에 직접 만들지 않고 Friendship라는 통과 타입을 만들어 연결하였다. 그리고 Friendship 타입에 친구 리스트와 관계를 받을 수 있는 필드를 추가하였다. 아래와 같은 경우는 기존 타입에 추가적인 정보가 필요할 때 사용할 수 있다. 친구 리스트를 나타내는 필드인 friends, 우정 지속기간인 howLong, 만난 위치인 whereWeMet 필드를 추가하였다.

  ```js
  type User {
    friends: [Friendship!]!
  }

  type Friendship {
    friends: [User!]!
    howLong: Int!
    whereWeMet: Location
  }
  ```

<br>

### # 인자(arguments)

<br>

- GrahpQL에서는 인자를 사용하여 다양한 일을 수행할 수 있다. 예를 들어 데이터의 순서를 변경할 수도 있고 데이터를 필터링하여 받아올 수도 있다. 또한 인자도 필드처럼 타입이 있어야한다. 스키마에서 사용할 수 있는 스칼라 타입이나 객체 타입으로 인자의 타입을 정할 수 있다. 또한 인자를 사용할 경우 대부분 특정 사용자나 정보를 받아오기 위해 사용하므로 필수적으로 전달해야하는 경우가 많다. 그렇기 때문에 null 값을 반환할 수 없는 필드로 정의하는 경우가 대부분이다. 아래 예시와 같은 경우 Query 타입에 allUsers와 allPhotos를 목록으로 반환하는 필드가 있는데 User 한명 혹은 Photo 한 장만 선택할 때 인자를 사용할 수 있다. 이 때 인자로 원하는 사용자나 사진에 대한 정보를 쿼리문 인자로 제공한다.

  ```js
  // 스키마
  type Query {
    ...
    User(githubLogin: ID!): User!
    Photo(id: ID!): Photo!
  }

  // 쿼리
  query {
    User(githubLogin: "Jay"){ // githubLogin이 Jay인 user의 이름과 아바타 데이터를 받아온다.
      name
      avatar
    }
  }

  query {
    Photo(id: "14TH5B6NS4KIG3H4S"){ // id가 인자로 전달한 값에 맞는 사진의 데이터를 받아온다.
      name
      description
      url
    }
  }
  ```

<br>

### # 뮤테이션(Mutation) 타입

<br>

- 뮤테이션도 쿼리와 마찬가지로 스키마 안에 커스텀 타입을 정의해두어야 한다. 뮤테이션 요청이 완료된 후에는 생성 된 데이터를 응답으로 받는다.

  ```js
  // 스키마
  // 루트 mutation 타입에 추가하여 클라이언트에서 사용할 수 있도록 한다.
  schema {
    query: Query
    mutation: Mutation
  }

  // postPhoto 필드를 추가하여 사용자가 사진을 게시할 수 있도록 한다.
  // 사용자가 게시하는 사진의 name을 필수 값으로 들어오도록 하였다.
  type Mutation {
    postPhoto(
      name: String!
      description: String
      category: PhotoCategory = PORTRAIT
    ): Photo!
  }

  // 사용자가 사진을 게시할 때 해당 뮤테이션 요청이 전송된다.
  // 생성 된 사진의 ID는 데이터베이스에서 생성해 부여한다.
  mutation {
    postPhoto(name: "Sending the palisades") {
      id
      url
      created
      postedBy {
        name
      }
    }
  }
  ```

<br>

### # 인풋(input) 타입

<br>

- 인풋 타입은 인자에서만 사용되며 인풋 타입을 활용하면 인자 관리를 체계적으로 할 수 있으며 모든 필드에서 인자로 사용할 수 있다.

  ```js
  // 스키마
  // 인풋 타입 사용 전
  schema {
    query: Query
    mutation: Mutation
  }

  type Mutation {
    postPhoto(
      name: String!
      description: String
      category: PhotoCategory = PORTRAIT
    ): Photo!
  }

  // request
  mutation {
    postPhoto(name: "Sending the palisades") {
      id
      url
      created
      postedBy {
        name
      }
    }
  }
  ```

  ```js
  // 스키마
  // 인풋 타입 사용 후
  schema {
    query: Query
    mutation: Mutation
  }

  input PostPhotoInput {
    name: String!
    description: String
    category: PhotoCategory = PORTRAIT
  }

  type Mutation {
    postPhoto(input: PostPhotoInput!): Photo!
  }

  // request
  mutation newPhoto($input: PostPhotoInput!){
    postPhoto(input: $input) {
      id
      url
      created
    }
  }
  ```

  ```json
  // response
  {
    "input": {
      "name": "Hanging at the Arc",
      "description": "Sunny on the deck of the Arc",
      "category": "LANDSCAPE"
    }
  }
  ```

<br>

### # 리턴(return) 타입

<br>

- 리턴 타입 또한 지정할 수 있다.

  ```js
  // 스키마
  // 로그인 시도 시 사용자 코드를 전달하여 유효하다면 user, token 정보가 담긴 객체를 반환하는 예시이다.
  type AuthPayload {
    user: User!
    token: String!
  }

  type Mutation {
    ...
    githubAuth(code: String!): AuthPayload!
  }
  ```

<br>

### # 서브스크립션(Subscription) 타입

<br>

- 서브스크립션은 구독 개념으로 뮤테이션이 실행될 때 마다 그 정보를 클라이언트에서 받아볼 수 있도록 만들 수 있다. 실시간 데이터를 다루기에 좋은 방법이다.

  ```js
  // 스키마
  // 커스텀 Subscription 객체를 만든 뒤 newPhoto와 newUser를 구독하는 예시이다. 만약 새로운 사진이 게시되면 newPhoto를 구독 중인 클라이언트는 모두 새로운 사진에 대한 알림을 받게 된다.
  schema {
    query: Query
    mutation: Mutation
    subscription: Subscription
  }

  type Subscription {
    newPhoto: Photo!
    newUser: User!
  }
  ```

- 서브스크립션에서도 인자를 사용할 수 있다. 인자를 사용하여 구독하는 쪽에서 원하는 데이터만 필터링하여 받아볼 수 있다.

  ```js
  // 스키마
  // 인자를 사용하여 생성되는 사진 중 카테고리가 ACTION인 사진의 데이터만 필터링하여 받는 예시이다.
  schema {
    query: Query
    mutation: Mutation
    subscription: Subscription
  }

  type Subscription {
    newPhoto(category: PhotoCategory): Photo!
    newUser: User!
  }

  subscription {
    newPhoto(category: "ACTION"){
      id
      name
      url
      postedBy {
        name
      }
    }
  }
  ```

<br>

### # 스키마 주석 (descriptions)

<br>

- 타입 전체에 descriptions을 사용할 때는 삼중따옴표, 타입 필드별 descriptions을 사용할 때는 따옴표를 사용할 수 있다.

  ```js
  const typeDefs = gql`
    """
    a cat astronaut
    """
    type SpaceCat {
      "the name of the cat"
      name: String!
      age: Int
      missions: [Mission]
    }
  `;
  ```

<br>

### # 리졸버(Resolver)

<br>

- 리졸버는 특정 필드의 데이터를 반환하는 함수이다. 스키마에 정의된 타입과 형태에 따라 데이터를 반환한다. 스키마에는 사용자가 작성할 수 있는 쿼리를 정의해두고, 타입 간의 연관 관계를 적어둔다. 데이터 요구 사항에 대한 내용은 들어있지만 실제로 데이터를 가져오는 일은 리졸버의 몫이다. 모든 필드는 그에 대응하는 리졸버 함수가 있어야 하며, 이들 함수는 스키마의 규칙을 따라야만 한다. 리졸버는 비동기로 작성할 수 있으며 REST API, 데이터베이스, 혹은 기타 서비스의 데이터를 가져오거나 업데이트 작업을 할 수 있다.

  ```js
  import { ApolloServer } from "apollo-server";

  // 스키마
  const typeDefs = `
      type Query {
          totalPhotos: Int!
      }
  `;

  // 리졸버
  const resolvers = {
    Query: {
      totalPhotos: () => 42,
    },
  };

  // 서버 인스턴스 생성
  const server = new ApolloServer({
    typeDefs,
    resolvers,
  });

  // 서버 구동
  server
    .listen()
    .then(({ url }) => console.log(`GraphQL Service running on ${url}`));
  ```

<br>

- 리졸버 함수는 기본적으로 4개의 인자를 받는다.

  1. parent: 이 필드의 부모 필드의 리졸버가 리턴한 객체이다. 참고로 부모 필드에 대한 리졸버가 자식 필드에 대한 리졸버보다 먼저 실행된다. 예를 들어 아래와 같은 쿼리에서 character에 대한 리졸버, weapon에 대한 리졸버가 있을 때 weapon에 대한 리졸버의 parent에는 character에 대한 리졸버 함수가 리턴한 객체가 담기게 되는 것이다. 리졸버 체인의 관점에서 이야기하면 리졸버 체인에서 이전에 있는 리졸버가 리턴한 객체를 의미한다. 이 객체를 활용해서 현재 리졸버가 내보낼 값을 조절 할 수 있다.

     ```js
     query character(id: $id) {
       weapon {
         name
         price
       }
     }
     ```

  2. args: Query, Mutation 실행 시 인자로 넣은 값이다.

  3. context: 모든 리졸버에게 전달 되는 값, 주로 미들웨어를 통해 입력된 값들이 들어있다. 즉 리졸버에서 전역적으로 사용가능한 변수라고 볼 수 있다. ApolloServer에서는 context 초기화 함수를 다음과 같이 집어 넣어서 사용할 수 있다.

     ```js
     // Constructor
     const server = new ApolloServer({
       typeDefs,
       resolvers,
       context: ({ req }) => ({
         authScope: getScope(req.headers.authorization),
       }),
     });

     // Example resolver
     (parent, args, context, info) => {
       if (context.authScope !== ADMIN)
         throw new AuthenticationError("not admin");
       // Proceed
     };
     ```

  4. info: 스키마 정보와 더불어 현재 쿼리의 특정 필드 정보를 가지고 있다. 잘 사용하지 않는 필드이다.

<br>

## # 관련 hooks

<br>

### # useQuery

<br>

- query를 실행할 때 사용한다.

  ```js
  // 구조 분해한 data는 useQuery의 결과 값이다. data 외에도 loading, error 등이 있다.
  const { data: userPinnedVideoStatus } = useQuery(
    ReadIsPinnedVideoOpenFieldDocument, // 실행 할 query 이다.
    {
      skip: !userId, // userId가 없는 경우 쿼리가 실행되지 않고 스킵된다.
      variables: {
        // query 실행 시 변수에 전달되는 값이다.
        userId: userId,
      },
    }
  );
  ```

<br>

### # useLazyQuery

<br>

- 일반적인 query는 컴포넌트가 마운트 및 렌더링되고 useQuery가 호출되면 자동으로 실행된다. 하지만 useMutation과 같이 원하는 시점에 query를 실행할 수 있도록 useLazyQuery를 사용할 수 있다. 즉 쿼리 지연을 위해 사용한다.

  ```js
  // getClubUserData를 사용해 원하는 시점에 query를 실행할 수 있다.
  const [getClubUserData, { data: clubData }] = useLazyQuery(
    ReadClubUserBasicDataDocument, // 실행 할 query 이다.
    {
      onCompleted: () => setLoading(false), // 쿼리 실행이 성공한 후 처리를 할 수 있다.
    }
  );
  ```

<br>

### # useMutation

<br>

- mutation을 실행할 때 사용한다.

  ```js
  // updateUser를 사용해 원하는 시점에 mutation을 실행할 수 있다.
  const [updateUser, { loading: updateLoading }] = useMutation(
    UpdatePlayerUserDocument, // 실행 할 mutation 이다.
    {
      update: (cache) => {
        cache.modify({
          // 캐시 데이터를 관리할 때 사용한다.
          id: "ROOT_QUERY", // id는 수정해야 할 캐시 데이터를 가리킨다.
          fields: {
            // fields는 함수 목록으로 수정이 필요한 각 필드의 함수를 지정한다. 각 필드 함수는 현재 필드 값을 인수로 받으며 해당 필드의 신규 값을 반환한다.
            player: () => {},
          },
        });
      },
    }
  );
  ```

<br>

### # useQuery vs useMutation

<br>

1. useQuery는 객체를 반환하지만 useMutation은 배열은 반환한다.

2. useQuery는 쿼리를 보내는 데 사용되는 반면 useMutation은 뮤테이션을 보내는데 사용한다.

3. useQuery는 컴포넌트 렌더링에서 자동으로 실행되는 반면 useMutation 후크는 뮤테이트 함수를 트리거하는 데 필요한 뮤테이션을 반환한다.

<br>

## # GraphQL 클라이언트

<br>

### # 아폴로 클라이언트

<br>

- 아폴로 클라이언트는 클라이언트에서 서버로 요청을 보내고 받는 것에 특화되어 있다. 아폴로 클라이언트를 사용해 GraphQL 서비스로 향하는 모든 네트워크 요청을 관리할 수 있으며 성능 향상을 위해 요청에 관한 응답 결과를 로컬 캐시에 자동으로 저장하고 요청 처리를 캐시로 위임한다.

<br>

### # 캐시 방침 설정

<br>

- fetchPolicy 프로퍼티를 사용하면 아폴로 클라이언트가 데이터를 찾아보는 장소를 지정할 수 있다. 데이터를 찾아보는 장소는 캐시 혹은 네트워크 요청 둘 중 하나가 된다.

  ```js
  const { data } = useQuery(ReadChangeModeDocument, {
    fetchPolicy: "cache-only",
  });
  ```

  1. cache-first : 기본 값, 이 상태에서 클라이언트는 캐시 내부만 들여다 본다. 만약 네트워크 요청 없이도 작업 처리가 가능하다면 캐시만 보고 끝난다. 그러나 쿼리에서 처리해야 할 데이터가 캐시에 없다면 네트워크 요청을 보낸다.

  2. cache-only : 클라이언트로 하여금 캐시만 보도록 강제하여 절대 네트워크 요청은 보내지 않는다. 만약 쿼리를 충족시키는 데이터가 캐시에 없다면 에러를 반환한다.

  3. cache-and-network : 요청 즉시 캐시를 우선으로 쿼리 처리 시도가 이루어지며 캐시 안의 데이터와는 별개로 최신 데이터를 가져오기 위해 네트워크 요청도 항상 추가로 보낸다.

  4. network-only : 쿼리를 처리할 때 네트워크 요청만 사용한다.

  5. no-cache : 항상 네트워크 요청을 사용해 데이터를 처리하고 응답 결과를 캐싱하지 않는다.

<br>

### # 로컬 앱 상태 관리

<br>

- readQuery : readQuery를 사용해 로컬 앱 상태를 캐시에서 바로 읽는다.

  ```js
  const cache = client.readQuery({
    query: ReadMapFilterLogDocument,
  });
  ```

- writeQuery : writeQuery를 사용해서 캐시의 로컬 앱 상태를 바로 업데이트한다.

  ```js
  client.writeQuery({
    query: ReadSearchLogDocument,
    data: {
      searchLog: {
        lastSearchType: null,
        lastPlayerSearchOption: null,
        lastClubSearchOption: null,
      },
    },
  });
  ```

- onResetStore : 모든 로컬 앱 상태 데이터를 삭제할 수 있다. 쿼리가 실행되면 로컬 앱 상태를 변경해야 한다. onResetStore는 저장소가 초기화 된 후에 호출되는 콜백 함수를 정의할 수 있다.

  ```js
  _apolloClient.onResetStore(() => {
    console.log("do something on onResetStore !");
    return new Promise(() => {
      // do some Reset task...
      console.log("reset task");
    });
  });
  ```

<br>
