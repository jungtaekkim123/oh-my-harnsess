# 파일 입출력 — SimTalk 2.0 Code Examples

> Cross-reference: `references/13-fn-os.md` and `references/20-fn-misc-model.md` for full function signatures

---

## Pattern 1: 텍스트 파일 읽기 — readStringFromFile + 행 단위 파싱

**Use when:** 외부 텍스트 파일을 읽어 시뮬레이션 데이터로 활용할 때

```simtalk
// 전체 파일을 문자열로 읽기
var filePath := getCurrentDirectory + "config.txt"
var content : string := readStringFromFile(filePath)
print content

// 줄 단위로 파싱 (줄바꿈 = \r\n 또는 \n)
var lines : string[] := splitString(content, strChr(13) + strChr(10))
// strChr(13) = CR, strChr(10) = LF

for var i := 1 to lines.dim
    var line := strTrim(lines[i])
    if strLen(line) > 0  // 빈 줄 건너뛰기
        print "Line ", i, ": ", line
    end
next

// 키-값 형식 설정 파일 파싱 (key=value)
var configContent := readStringFromFile("settings.txt")
var configLines := splitString(configContent, strChr(13) + strChr(10))

for var i := 1 to configLines.dim
    var line := strTrim(configLines[i])
    if strLen(line) = 0
        continue  // 빈 줄 건너뛰기
    end
    var eqPos := strLPos("=", line)
    if eqPos > 0
        var key := strTrim(strCopy(line, 1, eqPos - 1))
        var val := strTrim(strCopy(line, eqPos + 1, strLen(line)))
        print key, " → ", val
    end
next
```

**Key points:**
- `readStringFromFile`은 파일 전체를 하나의 문자열로 반환
- BOM(Byte Order Mark)이 있으면 자동 처리되어 반환 문자열에 포함되지 않음
- 줄바꿈 구분자는 OS에 따라 `\r\n`(Windows) 또는 `\n`(Unix) — 양쪽 모두 처리 권장

---

## Pattern 2: 텍스트 파일 쓰기 — writeStringToFile

**Use when:** 시뮬레이션 결과를 텍스트/로그 파일로 내보낼 때

```simtalk
// 기본 쓰기 — 파일이 이미 있으면 덮어씀
var output := "Simulation Report"
writeStringToFile(output, "C:\Temp\report.txt")

// 여러 줄 쓰기 — 줄바꿈 포함 문자열 생성
var newline := strChr(13) + strChr(10)  // \r\n
var report := "=== Simulation Results ===" + newline
report += "Date: 2024-03-15" + newline
report += "Total Parts: 1500" + newline
report += "Throughput: 125.5 parts/hour" + newline
writeStringToFile(report, "C:\Temp\results.txt")

// 추가 모드 (Append) — 로그 파일에 라인 추가
var logLine := "14:30:00 | Station_A | Part processed"
writeStringToFile(logLine, "C:\Temp\sim_log.txt", true)
// Append=true이면 기존 내용 뒤에 줄바꿈 + 텍스트 추가

// 인코딩 지정
// UTF-8 (기본값, BOM 포함)
writeStringToFile("Hello", "output_utf8.txt")
// UTF-8 without BOM
writeStringToFile("Hello", "output_no_bom.txt", false, "")
// UTF-16
writeStringToFile("Hello", "output_utf16.txt", false, "Unicode")

// JSON 데이터를 파일로 저장
var data : json
data["Name"] := "ProductionLine_A"
data["Throughput"] := 1234
data["Efficiency"] := 0.956
// JSON은 BOM 없이 저장 권장
writeStringToFile(data.asString, "D:\output\config.json", false, "")
```

**Key points:**
- `Append` 파라미터를 `true`로 설정하면 기존 파일 끝에 추가 (로그에 적합)
- 인코딩 기본값은 `"UTF-8"` (BOM 포함), 빈 문자열 `""`은 BOM 없는 UTF-8
- JSON 파일 저장 시 BOM 없이(`""`) 저장해야 외부 파서 호환성 확보

---

## Pattern 3: CSV 파일 파싱 — splitString으로 행/열 분리

**Use when:** CSV 형식의 외부 데이터를 읽어 테이블에 적재할 때

```simtalk
// CSV 파일 읽기 및 파싱
var csvContent := readStringFromFile("C:\Data\production_log.csv")
var newline := strChr(13) + strChr(10)
var rows : string[] := splitString(csvContent, newline)

// 첫 행은 헤더 — 나머지 데이터 처리
for var rowIdx := 2 to rows.dim
    var line := strTrim(rows[rowIdx])
    if strLen(line) = 0
        continue
    end

    var cols : string[] := splitString(line, ";")
    // cols[1] = 파트명, cols[2] = 수량, cols[3] = 시간

    DataTable[1, rowIdx - 1] := cols[1]                    // 문자열
    DataTable[2, rowIdx - 1] := str_to_num(cols[2])        // 숫자 변환
    DataTable[3, rowIdx - 1] := str_to_num(cols[3])        // 숫자 변환
next

// 빈 셀이 포함된 CSV 처리: KeepEmptyItems 사용
var sparseRow := "A;;B;;C"
var fields := splitString(sparseRow, ";", true)
print fields         // [A, , B, , C] — 빈 필드도 유지

// splitStringToNum으로 숫자 CSV 직접 파싱
var numRow := "10.5;20.3;30.1;40.8"
var values : real[] := splitStringToNum(numRow, ";")
values.copyToTableColumn(DataTable, 2)

// CSV 생성 및 내보내기
var outputLines : string[]
outputLines.append("PartName;Count;CycleTime")  // 헤더
for var r := 1 to DataTable.yDim
    var row : string[]
    row.append(to_str(DataTable[1, r]))
    row.append(to_str(DataTable[2, r]))
    row.append(num_to_str(DataTable[3, r], "0.00"))
    outputLines.append(row.join(";"))
next
var csvOutput := outputLines.join(strChr(13) + strChr(10))
writeStringToFile(csvOutput, "C:\Data\export.csv")
```

**Key points:**
- `splitString`의 세 번째 인자 `KeepEmptyItems`로 빈 셀 처리 여부 제어
- 숫자 변환은 `str_to_num()`, 포맷팅된 출력은 `num_to_str()`
- CSV 내보내기 시 `join`과 배열 조합으로 효율적으로 행 생성

---

## Pattern 4: 파일 존재 확인 — existsFile, 경로 조합

**Use when:** 파일 읽기/쓰기 전 안전하게 존재 여부를 확인할 때

```simtalk
// 단일 파일 존재 확인
var fileName := "MyDataTable.tab"
if not existsFile(fileName)
    DataTable.writeFile(fileName)
    print "파일 생성 완료: ", fileName
else
    print "파일이 이미 존재합니다: ", fileName
end

// 절대 경로로 확인
if existsFile("C:\Data\config.xml")
    print "설정 파일을 찾았습니다"
end

// 폴더 존재 확인 (파일뿐 아니라 폴더도 가능)
if existsFile("C:\Data\Output")
    print "출력 폴더가 존재합니다"
end

// 현재 작업 디렉토리 기반 경로 조합
var baseDir := getCurrentDirectory
var dataPath := baseDir + "data\input.csv"
if existsFile(dataPath)
    var content := readStringFromFile(dataPath)
    print "파일 로드 완료. 크기: ", strLen(content), " bytes"
else
    print "파일을 찾을 수 없습니다: ", dataPath
end

// 모델 파일 경로 활용
var modelDir := modelFile
print "현재 모델: ", modelDir
```

**Key points:**
- `existsFile`은 파일과 **폴더** 모두 확인 가능
- 파일 없이 `readStringFromFile`을 호출하면 런타임 에러 발생 — 반드시 사전 확인
- `getCurrentDirectory`는 Plant Simulation의 현재 작업 폴더를 반환

---

## Pattern 5: 파일 복사 및 삭제 — copyFile, deleteFile

**Use when:** 백업 생성, 임시 파일 정리, 파일 이동 등 파일 시스템 작업이 필요할 때

```simtalk
// 파일 복사
var success := copyFile("C:\Data\source.txt", "C:\Backup\source.txt")
if success
    print "파일 복사 성공"
else
    print "파일 복사 실패"
end

// 모델 결과 백업
var timestamp := to_str(currentEventCtl.SimTime)
var backupName := "C:\Backup\results_" + timestamp + ".csv"
copyFile("C:\Data\results.csv", backupName)

// 파일 삭제 — 반환값 0이면 성공
var errCode := deleteFile("C:\Temp\temp_output.txt")
if errCode = 0
    print "임시 파일 삭제 완료"
else
    print "삭제 실패. 에러코드: ", errCode
end

// 안전한 삭제 — 존재 확인 후 삭제
var targetFile := "C:\Temp\old_log.txt"
if existsFile(targetFile)
    deleteFile(targetFile)
    print "파일 삭제: ", targetFile
end

// system 명령으로 삭제 (DOS 명령)
if system("del C:\temp\file.txt") = 0
    print "file deleted"
end
```

**Key points:**
- `copyFile`은 `boolean` 반환 (성공/실패)
- `deleteFile`은 Windows 에러코드를 `integer`로 반환 (0 = 성공)
- "Prohibit access to the computer" 보안 설정이 활성화되면 모델 폴더 외부 접근 제한

---

## Pattern 6: 경로 다루기 — getCurrentDirectory, makePathRelative, browseForFolder

**Use when:** 작업 폴더를 관리하거나 사용자에게 폴더를 선택하게 할 때

```simtalk
// 현재 작업 디렉토리 확인 및 변경
var cwd := getCurrentDirectory
print "현재 작업 폴더: ", cwd

// 작업 폴더 변경
var changed := setCurrentDirectory("C:\SimData")
if changed
    print "작업 폴더 변경 성공"
end

// 절대 경로 → 상대 경로 변환
var absPath := ".Models.Model.Station1"
var relPath := makePathRelative(absPath)
print relPath        // 현재 메서드 기준 상대 경로

// 사용자에게 폴더 선택 다이얼로그 표시
var selectedFolder := browseForFolder("데이터 폴더를 선택하세요:")
if strLen(selectedFolder) > 0
    print "선택된 폴더: ", selectedFolder
    setCurrentDirectory(selectedFolder)
end

// 파일 선택 다이얼로그 — 필터 적용
var selectedFile := selectFileForOpen("CSV Files (*.csv)|*.csv||")
if selectedFile /= ""
    var csvData := readStringFromFile(selectedFile)
    print "파일 로드 완료: ", selectedFile
end

// 저장 다이얼로그
var savePath := selectFileForSave("Text Files (*.txt)|*.txt||", "report.txt")
if savePath /= ""
    writeStringToFile("Simulation complete", savePath)
end

// 폴더 내 파일 목록 조회
var allFiles := getFilesOfFolder("C:\Data\*.csv")
// allFiles는 list 타입 — CSV 파일 목록 반환

// 모델 파일 경로 활용
var modelPath := modelFile
print "현재 모델 파일: ", modelPath
// 모델 폴더 추출
var lastSlash := strRpos("\", modelPath)
var modelFolder := strCopy(modelPath, 1, lastSlash)
print "모델 폴더: ", modelFolder
```

**Key points:**
- `browseForFolder`는 Windows 표준 폴더 선택 다이얼로그를 표시
- `selectFileForOpen`/`selectFileForSave`는 파일 필터 문자열을 `||`로 종결
- `makePathRelative`는 시뮬레이션 객체 경로를 상대 경로로 변환 (파일 경로가 아님)
- `getFilesOfFolder`는 와일드카드(`*`, `?`) 지원하며 `list` 타입 반환
