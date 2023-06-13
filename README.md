# jquery_test
```
$('form').submit(function(event) {
    var sum = parseInt($('#fieldB').val()) + parseInt($('#fieldC').val());
    if (sum !== parseInt($('#fieldA').val())) {
      alert('Field A must be the sum of Fields B and C');
      event.preventDefault();
    }
  });
```

```
<form>
  <label for="fieldB">Field B:</label>
  <input type="number" id="fieldB" name="fieldB" required>

  <label for="fieldC">Field C:</label>
  <input type="number" id="fieldC" name="fieldC" required>

  <label for="fieldA">Field A:</label>
  <input type="number" id="fieldA" name="fieldA" required>

  <button type="submit">Submit</button>
</form>

<script src="https://code.jquery.com/jquery-3.6.0.min.js"></script>
<script>
  // Function to validate the fields
  function validateFields() {
    var valueB = parseInt($('#fieldB').val(), 10);
    var valueC = parseInt($('#fieldC').val(), 10);
    var valueA = parseInt($('#fieldA').val(), 10);

    if (valueB + valueC === valueA) {
      // Validation passed, remove any error indication
      $('#fieldA').removeClass('error');
    } else {
      // Validation failed, add error indication
      $('#fieldA').addClass('error');
    }
  }

  // Event listener for field changes
  $('#fieldB, #fieldC, #fieldA').on('input', function() {
    validateFields();
  });
</script>

```
