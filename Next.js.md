# Next.js

### Navigate

`pages/index.tsx`가 기본 첫화면이다.(`/`로 접속하면 나오는 화면)
보여주고 싶은 Page가 있다면 `pages` 폴더에 파일을 만들어 넣는다.

예) `localhost:3000/user/login`을 보여주고 싶다면

1. `pages` 폴더 안에 `user` 폴더를 만들고, `login.tsx`를 만든다.
2. `localhost:3000/user/login`을 주소창에 입력하면 해당 화면이 출력된다!

외부의 링크를 걸때는 `<a>` 를 사용해도 무방하지만, 내부에서 페이지 이동을 할 때는 `next/link`에서 제공하는 `Link` 컴포넌트를 사용해서 이동시켜줘야 한다.

> `<Link>` allows you to do client-side navigation to a different page in the application.

:exclamation: `Link` 컴포넌트를 사용할 때는 내부의 이동경로를 `a`태그가 아닌 `Link` 컴포넌트에 작성해줘야 한다.

```tsx
import Link from 'next/link'

export default function FirstPost() {
  return (
    <>
      <h1>First Post</h1>
      <h2>
        <Link href="/">
          <a>Back to home</a>
        </Link>
      </h2>
    </>
  )
}
```

:exclamation: 만약 `className`과 같은 추가할 속성이 있다면 `Link`가 아닌 `a`태그에 추가 할 것.



### Assets

Static assets(이미지 같은) 파일들은 `public` 폴더에 추가하고, 아래처럼 경로를 적어주면 된다.

```tsx
<img src="/vercel.svg" alt="Vercel Logo" className="logo" />
```

Navigate의 root가 되는 `pages`처럼 `public`은 정적 파일들의 root라고 생각하면 된다.



### Pre-rendering and Data Fetching

기본적으로 Next.js에서는 모든 페이지를 미리 랜더링하고, 자바스크립트를 통해 client-side에서 페이지 이동을 한다. 단, JS 코드는 랜더링에 필요한 최소한만 생성하고 실제 요청한 페이지가 로딩될 때 모든 코드가 실행된다.
:arrow_right: 더 나은 preformance 와 SEO를 위함



미리 랜더링 할 때 필요한 데이터가 있다면(파일 시스템에 액세스하거나, 외부 API를 가져 오거나, 빌드시 데이터베이스에 쿼리를 보내거나) `getStaticProps`를 이용해 정적 생성을 할 수 있다. 이 함수는 최초에 실행된다.

```jsx
export default function Home(props) { ... }

export async function getStaticProps() {
  // Get external data from the file system, API, DB, etc.
  const data = ...

  // The value of the `props` key will be
  //  passed to the `Home` component
  return {
    props: ...
  }
}
```



`getStaticProps`에 직접 가져오는 함수를 적어도 되고, 분리해서 적용시켜도 된다. 만약 함수를 분리해서 적용할 거라면 분리한 함수를 `getStaticProps` 안에서 불러와주면 된다.

```tsx
export function getSortedPostsData() {
    const datas = []
    //...function
    return datas;
}

export async function getStaticProps() {
  const allPostsData = getSortedPostsData()
}
```

또, `getStaticProps`는 필요한 페이지에서 불러와서 쓰면 된다.