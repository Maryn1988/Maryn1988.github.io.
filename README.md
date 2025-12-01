<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">
<html xmlns="http://www.w3.org/1999/xhtml">
<head>

  <meta http-equiv="Content-Type" content="text/html; charset=cp1251" />
  <title>������ ���������� ������� (��������� ����)</title>
  <style>
    body {
      margin: 0;
      padding: 0;
      background: #0f172a; /* ����� ��� */
      color: #e5e7eb;
     // font-family: system-ui, -apple-system, BlinkMacSystemFont, "Segoe UI", sans-serif;
      display: flex;
      align-items: center;
      justify-content: center;
      height: 100vh;
    }

    .wrapper {
      max-width: 900px;
      padding: 24px 32px;
      border-radius: 14px;
      background: rgba(15, 23, 42, 0.9);
      border: 1px solid rgba(148, 163, 184, 0.4);
      box-shadow: 0 24px 60px rgba(15, 23, 42, 0.8);
    }

    .label {
      font-size: 13px;
      letter-spacing: 0.16em;
      text-transform: uppercase;
      color: #38bdf8;
      margin-bottom: 8px;
    }

    .line {
      font-size: 26px;
      font-weight: 600;
      white-space: nowrap;
      overflow: hidden;
      border-right: 2px solid #facc15; /* ������ */
    }

    @keyframes blink {
      0%, 49%   { border-color: #facc15; }
      50%, 100% { border-color: transparent; }
    }

    .line.typing-done {
      animation: blink 0.9s step-end infinite;
    }
  </style>
</head>
<body>
  <div class="wrapper">
    <div class="label">Notion-�����������</div>
    <div id="typing" class="line"></div>
  </div>

  <script>
    // ����� ����� �����, ������� ����� ���������� �� �������
    const phrases = [
      "����� �������� � ������� ������� ������� � ����� Notion.",
      "������ �������� ������� � ������� ������������ ��� ���� ������.",
      "����������� ��������, ����� �� ������� ������ ������� �� ������."
    ];

    const el = document.getElementById("typing");
    const typeSpeed = 70;   // �������� ������ (�� �� ������)
    const eraseSpeed = 40;  // �������� �������� (�� �� ������)
    const holdTime = 1500;  // ����� ����� ������������� ����� (��)

    let phraseIndex = 0;
    let charIndex = 0;
    let isDeleting = false;

    function typeLoop() {
      const currentPhrase = phrases[phraseIndex];

      if (!isDeleting) {
        // ��������
        el.textContent = currentPhrase.slice(0, charIndex + 1);
        charIndex++;

        if (charIndex === currentPhrase.length) {
          // ����� ����������
          el.classList.add("typing-done");
          setTimeout(() => {
            isDeleting = true;
            el.classList.remove("typing-done");
            typeLoop();
          }, holdTime);
          return;
        }

        setTimeout(typeLoop, typeSpeed);
      } else {
        // �������
        el.textContent = currentPhrase.slice(0, charIndex - 1);
        charIndex--;

        if (charIndex === 0) {
          // ��������� � ��������� �����
          isDeleting = false;
          phraseIndex = (phraseIndex + 1) % phrases.length;
          setTimeout(typeLoop, typeSpeed);
          return;
        }

        setTimeout(typeLoop, eraseSpeed);
      }
    }

    typeLoop();
  </script>
</body>
</html>
