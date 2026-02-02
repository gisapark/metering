<!doctype html>
<html lang="ko">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width,initial-scale=1" />
  <title>검침 검증 앱 (화면 전용)</title>
  <link rel="stylesheet" href="styles.css" />
  <!-- 엑셀 읽기용 SheetJS (인터넷 필요) -->
  <script defer src="https://cdn.jsdelivr.net/npm/xlsx@0.18.5/dist/xlsx.full.min.js"></script>
  <script defer src="app.js"></script>
</head>
<body>
  <header class="header">
    <h1>검침 검증 앱 (화면 전용)</h1>
    <p class="sub">엑셀 2개(기존 누적 + 이번달)를 올리면 화면에서 바로 “역전/0사용/급증/누락”을 보여줍니다. (엑셀 다운로드/저장은 없음)</p>
  </header>

  <main class="container">
    <section class="card">
      <h2>1) 파일 업로드</h2>
      <div class="grid2">
        <div class="field">
          <label>기존 누적 파일 (xlsx)</label>
          <input id="cumFile" type="file" accept=".xlsx,.xls" />
          <div class="hint">이전달(들) 지침이 들어있는 파일</div>
        </div>
        <div class="field">
          <label>이번달 검침 파일 (xlsx)</label>
          <input id="newFile" type="file" accept=".xlsx,.xls" />
          <div class="hint">이번달 지침이 들어있는 파일</div>
        </div>
      </div>

      <div class="grid2">
        <div class="field">
          <label>이번 달 (YYYY-MM)</label>
          <input id="targetMonth" type="text" placeholder="예: 2026-02" />
          <div class="hint">비우면 파일명/시트명에서 추정합니다.</div>
        </div>
        <div class="field">
          <label>중복 처리 (이번달에 같은 세대/종류가 여러 번 있으면)</label>
          <select id="dupPolicy">
            <option value="lastwins">마지막 값 사용</option>
            <option value="firstwins">첫 값 사용</option>
          </select>
        </div>
      </div>

      <div class="actions">
        <button id="analyzeBtn" class="btn" disabled>분석 시작</button>
      </div>
      <div class="status" id="status"></div>

      <details class="details">
        <summary>⚠ 버튼이 안 눌리는 경우</summary>
        <p class="sub2">
          이 앱은 엑셀을 읽기 위해 인터넷에서 라이브러러리를 불러옵니다.<br/>
          네트워크가 차단되어 있으면 “분석 시작”이 계속 비활성일 수 있어요.<br/>
          그럴 땐 GitHub Pages로 올려서 실행하면 가장 안정
