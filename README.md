<script>
    // १. तुमच्या Google Sheet चा ID येथे टाका
    const SHEET_ID = 'Setu Report'; 
    // २. शीटचे नाव (उदा. Sheet1)
    const SHEET_NAME = 'Setu Report'; 
    
    // Google Sheets API URL
    const SHEET_URL = `https://docs.google.com/spreadsheets/d/e/2PACX-1vSSSrez80ZuHamCAEkpUtD3G5o5oRQLNZV5YErVEAgh3ttUdZvKuEsc6QUjeB3Y6bqw_kKIolzgAxF0/pub?gid=1589437184&single=true&output=csv`;

    async function loadJsonData() {
      const btn = document.querySelector('.btn');
      const originalText = btn.innerHTML;
      
      try {
        // बटनवर लोडिंग दाखवा
        btn.innerHTML = '<span class="spinner"></span> डेटा शोधत आहे...';
        btn.disabled = true;

        // Google Sheet कडून डेटा मिळवा
        const response = await fetch(SHEET_URL);
        const text = await response.text();
        
        // Google Sheets कडून येणारा डेटा स्वच्छ करणे (surrounding text काढून टाकणे)
        const jsonText = text.substring(47).slice(0, -2);
        const data = JSON.parse(jsonText);
        
        // डेटा रोज (Rows) मध्ये रूपांतरित करा
        const rows = data.table.rows;
        
        // तुमच्या HTML मधील इनपुट व्हॅल्यू मिळवा
        const inputVal = document.getElementById("codeInput1").value.trim();

        if (!inputVal) {
          showNotification("कृपया अर्ज क्रमांक टाका.", "warning");
          resetButton();
          return;
        }

        // शीटमध्ये डेटा शोधणे
        let found = false;
        rows.forEach(row => {
          // समजा पहिल्या कॉलममध्ये (Index 0) अर्ज क्रमांक आहे
          const sheetCode = row.c[0] ? row.c[0].v.toString() : "";
          
          if (sheetCode === inputVal) {
            found = true;
            // जर डेटा सापडला तर डाऊनलोड फंक्शन कॉल करा
            downloadApplicationFile(sheetCode);
          }
        });

        if (!found) {
          showNotification("दिलेला अर्ज क्रमांक सापडला नाही. कृपया पुन्हा तपासा.", "error");
        }

      } catch (error) {
        console.error("Error fetching sheet data:", error);
        showNotification("Google Sheet मधून डेटा लोड करताना त्रुटी आली.", "error");
      } finally {
        resetButton();
      }

      function resetButton() {
        btn.innerHTML = originalText;
        btn.disabled = false;
      }
    }

    // नोटिफिकेशन फंक्शन (तुमच्या कोडमध्ये आधीपासून आहे असे गृहीत धरले आहे)
    function showNotification(message, type) {
      console.log(`${type.toUpperCase()}: ${message}`);
      // तुमच्या मूळ कोडमधील नोटिफिकेशन लॉजिक येथे असेल
    }

    // डाऊनलोड फंक्शन (तुमच्या index.html मधून घेतलेले)
    function downloadApplicationFile(applicationId) {
      if (!applicationId) {
        showNotification("अर्ज क्रमांक सापडला नाही.", "error");
        return;
      }
      
      const downloadLink = `https://cscservices.mahaonline.gov.in/Edistrict/Handler/GetFile.ashx?From=ApplicationStatus&ID=${applicationId}&sDist=529`;
      window.open(downloadLink, '_blank');
      showNotification(`अर्ज ${applicationId} साठी डाऊनलोड सुरू केला आहे!`, "success");
      
      // अलीकडील हालचाली अपडेट करा
      updateRecentActivity(applicationId); 
    }

    // पेज लोड झाल्यावर इनपुटवर फोकस करा
    window.onload = () => {
      if(document.getElementById("codeInput1")) {
        document.getElementById("codeInput1").focus();
      }
    };
</script>
