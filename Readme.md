
# Connect Form

Connect Form is a multipart / urlencoded form parsing middleware utilizing [node-formidable](http://github.com/felixge/node-formidable) behind the scenes.

## Examples

    var server = connect.createServer(
	    multipart({ keepExtensions: true }),
	    function(req, res, next){
		    // Form was submitted
	        if (req.form) {
		        // Do something when parsing is finished
		        // and respond, or respond immediately
		        // and work with the files.
	            req.form.onComplete = function(err, fields, files){
	                res.writeHead(200, {});
	                if (err) res.write(JSON.stringify(err.message));
	                res.write(JSON.stringify(fields));
	                res.write(JSON.stringify(files));
	                res.end();
	            };
	        // Regular request, pass to next middleware
	        } else {
	            next();
	        }
	    }
	);