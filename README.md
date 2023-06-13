# jquery_test
<!DOCTYPE html>
<html>
<head>
  <title>Form Fields Observation</title>
  <script src="https://code.jquery.com/jquery-3.6.0.min.js"></script>
</head>
<body>
  <label for="serverQty">Server Quantity:</label>
  <input type="number" id="physicalServerQty" readonly><br><br>

  <label for="primarySiteServers">Primary Site Servers:</label>
  <input type="number" id="primarySiteServers" min="0" readonly><br><br>

  <label for="secondarySiteServers">Secondary Site Servers:</label>
  <input type="number" id="secondarySiteServers" min="0" readonly><br><br>

  <label for="topology">Topology:</label>
  <select id="topology">
    <option value="">Please select a topology</option>
    <option value="2+2">2+2</option>
    <option value="2+1">2+1</option>
  </select><br><br>

  <script>
    function updateFields() {
      let primary = Math.max(0, parseInt($('#primarySiteServers').val()) || 0);
      let secondary = Math.min(primary, Math.max(0, parseInt($('#secondarySiteServers').val()) || 0));
      $('#primarySiteServers').val(primary);
      $('#secondarySiteServers').val(secondary);
      $('#physicalServerQty, #virtualServerQty').val(primary + secondary);
    }

    function setReadonlyStatus() {
      if($('#topology').length) {
        $('#primarySiteServers, #secondarySiteServers').prop('readonly', true);
      } else {
        $('#primarySiteServers, #secondarySiteServers').prop('readonly', false);
      }
    }

    $(document).ready(function() {
      setReadonlyStatus();

      // Create an observer instance linked to the callback function
      const observer = new MutationObserver(function(mutationsList, observer) {
        for(let mutation of mutationsList) {
          if (mutation.type === 'attributes' && mutation.attributeName === 'id') {
            setReadonlyStatus();
          }
        }
      });

      // Start observing the document with the configured parameters
      observer.observe(document.body, { attributes: true, subtree: true });

      $('#topology').on('change', function() {
        if(this.value === "") {
          $('#primarySiteServers, #secondarySiteServers').prop('readonly', false);
        } else {
          let values = this.value.split('+').map(Number);
          if(values.length === 2) {
            $('#primarySiteServers').val(values[0]);
            $('#secondarySiteServers').val(values[1]);
            $('#primarySiteServers, #secondarySiteServers').prop('readonly', true);
            updateFields();
          }
        }
      });

      $('#primarySiteServers, #secondarySiteServers').on('input', updateFields);
    });
  </script>
</body>
</html>
```
