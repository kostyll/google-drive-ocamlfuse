The configuration file is saved in `~/.gdfuse/default/config` (or `~/.gdfuse/label/config` if a label was specified on the command line). The parser is very simple and only accepts lines in the form `key=value`, without spaces, comments, or anything else.

### Content

Specifies if debug mode is turned on: if `true`, logs verbose output to `~/.gdfuse/default/gdfuse.log`, and logs every curl request to `~/.gdfuse/default/curl.log`:

    debug=false

Specifies the interval in seconds between queries to detect server-side changes:

    metadata_cache_time=60

Specifies if the filesystem is to be mounted read-only:

    read_only=false

Specifies the umask (i.e. the bitmask of  the  permissions  that  are  not present) mount option:

    umask=0o002

Specifies the Sqlite3 busy handler timeout in milliseconds:

    sqlite3_busy_timeout=500

Specifies whether to download Google Docs (these files are read-only, even if `read_only=false`):

    download_docs=true

Text document [[export format|Exportable-formats#valid-download-formats-for-text-documents]]:

    document_format=odt

Drawings [[export format|Exportable-formats#valid-download-formats-for-drawings]]:

    drawing_format=png

Forms [[export format|Exportable-formats#valid-formats-for-spreadsheets]]:

    form_format=ods

Presentations [[export format|Exportable-formats#valid-formats-for-presentations]]:

    presentation_format=pdf

Spreadsheets [[export format|Exportable-formats#valid-formats-for-spreadsheets]]:

    spreadsheet_format=ods

Maps export format (the only valid format is `desktop`):

    map_format=desktop

OAuth2 client ID (optional):

    client_id=

OAuth2 client secret (optional):

    client_secret=

OAuth2 verification code (optional). Useful when authorizing on a different machine.

    verification_code=

Conflict resolution strategy. In case of conflict (update on both sides), if
we set the `client` value, the application will always update the server
resource (client side wins). Otherwise, setting `server`, the application will
always maintain the server version of the resource (server side wins):

    conflict_resolution=server

Google Drive supports multiple files with the same name. This flag specifies
the behavior of `mv`: When set to `false`, `mv` behaves in the standard way,
overwriting (trashing) the target file if it exists. When set to `true`, `mv`
will always keep the target file:

    keep_duplicates=false

Specifies whether to display file extensions for Google Docs:

    docs_file_extension=true

Specifies the maximum cache size in MB:

    max_cache_size_mb=512

Specifies whether overwriting a file generates a new revision:

    new_revision=true

Specifies whether to permanently turn off CURL logging (even in debug mode). Set it to `true` to avoid a segmentation fault on some architectures:

    curl_debug_off=false

Specifies whether files removed from trash folder are permanently deleted (**WARNING**: permanently deleted files *cannot be recovered*, set it to `true` at your own risk):

    delete_forever_in_trash_folder=false

Specifies whether to directly stream large files (so that are no more cached):

    stream_large_files=false

Specifies the threshold (in megabytes) to detect large files:

    large_file_threshold_mb=16

Force export of Google Docs in the format specified above. Introduced as a workaround for [this bug](https://code.google.com/a/google.com/p/apps-api-issues/issues/detail?id=3713):

    force_docs_export=true

### Document export formats

`desktop` format creates a shortcut to the document that will be opened in the web browser for edit.

If you don't want to export a specific kind of docs, just remove the format portion. For example, if you have this line in your `config` file:

    drawing_format=

no drawings will be exported.

Note that if you change any export format, you will have to clear the cache (using `-cc` command line option).