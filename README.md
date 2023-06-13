# jquery_test

$('form').submit(function(event) {
    var sum = parseInt($('#fieldB').val()) + parseInt($('#fieldC').val());
    if (sum !== parseInt($('#fieldA').val())) {
      alert('Field A must be the sum of Fields B and C');
      event.preventDefault();
    }
  });
