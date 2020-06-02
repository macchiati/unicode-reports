# Unicode Reports

This is a work area for edcom.  Note that the actual reports are located at: <https://www.unicode.org/reports/>

Browsing within this repo you can see the source HTML files for the various reports. To view one of the HTML files from this repo as a Web page, go to <https://unicode-org.github.io/unicode-reports/> and browse from there.

Note; while viewing this page on githum.com, ignore the raw html / script below. (It's used to generate the browseable view on unicode-org.github.io.)

### Direct Links to HTML Views of the Head for the Reports in the Repository

<ul id='reports'>
    <i>(list of reports here)</i>
</ul>

<script
  src="https://code.jquery.com/jquery-3.5.1.min.js"
  integrity="sha256-9/aliU8dGd2tb6OSsuzixeV4y/faTqgFtohetphbbj0="
  crossorigin="anonymous"></script>
<script>
    $(function() {
        $('#reports').empty();
        $('#reports').append('Loading…');
      $.get('https://api.github.com/repos/unicode-org/unicode-reports/contents/')
      .then(data => {
        $('#reports').empty();
        const col = new Intl.Collator([], {numeric: true});
        data.sort((a,b)=>col.compare(a.name,b.name));
        data.forEach(({name, type}) => {
            if(type === 'dir' && /^tr[0-9]+$/.test(name)) {
                $('#reports').append(
                    $('<li>').append(
                        $('<a>', {
                            text: `${name}`,
                            href: `https://unicode-org.github.io/unicode-reports/${name}/${name}.html`
                        })));
            }
        });
      }).catch((err) => $('#reports').append('Err: ' + err.message));
    });
</script>
