# graphics

#사용법
p5.js로 실행

index.html이동

코드 붙여넣기

실행


<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Speech Recognition with ml5.js</title>
    <!-- p5.js -->
    <script src="https://cdnjs.cloudflare.com/ajax/libs/p5.js/1.4.0/p5.js"></script>
    <!-- ml5.js -->
    <script src="https://unpkg.com/ml5@latest/dist/ml5.min.js"></script>
</head>
<body>
    <h2>Speech Recognition</h2>
    <p>마이크에 말할 준비가 되었으면 아래 버튼을 클릭하세요.</p>
    <button onclick="startSpeechRecognition()">음성 인식 시작</button>
    <p id="speech"></p>

    <script>
        let speechRec;

        function startSpeechRecognition() {
            // 사용자에게 오디오 액세스를 요청
            navigator.mediaDevices.getUserMedia({ audio: true })
                .then(function(stream) {
                    // 오디오 액세스가 허용되면 음성 인식 객체 생성
                    speechRec = ml5.speechRec();
                    // 음성 인식 시작
                    speechRec.start();
                    // 음성 인식 결과를 처리할 콜백 함수 등록
                    speechRec.onResult = showResult;
                    // 음성 인식 결과를 사용자에게 알림
                    document.getElementById('speech').innerText = '음성 인식이 시작되었습니다. 마이크에 말하세요.';
                })
                .catch(function(err) {
                    console.error('오디오 액세스 권한이 거부되었습니다:', err);
                    // 오디오 액세스가 거부되면 메시지를 표시하여 사용자에게 허용을 요청
                    document.getElementById('speech').innerText = '오디오 액세스를 허용해주세요.';
                });
        }

        function showResult() {
            // 음성 인식 결과를 가져와서 표시
            if (speechRec.resultValue) {
                document.getElementById('speech').innerText = '당신이 말한 내용: ' + speechRec.resultString;
            }
        }
    </script>
</body>
</html>
