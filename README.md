Back in the early days of the web there was this wonderful Perl library
called CGI, many people only learned Perl because of it.
It was simple enough to get started without knowing much about the language
and powerful enough to keep you going, learning by doing was much fun.
While most of the techniques used are outdated now, the idea behind it is
not.
Mojolicious is a new attempt at implementing this idea using state of the art
technology.

Features
--------

* An amazing MVC web framework supporting a simplified single file mode
  through Mojolicious::Lite.

* Very clean, portable and Object Oriented pure Perl API without any hidden
  magic and no requirements besides Perl 5.8.1.

* Full stack HTTP 1.1 and WebSocket client/server implementation with IPv6,
  TLS, IDNA, pipelining, chunking and multipart support.

* Builtin async IO and prefork web server supporting epoll, kqueue, hot
  deployment and UNIX domain socket sharing, perfect for embedding.

* CGI, FastCGI and PSGI support.

* Fresh code, based upon years of experience developing Catalyst.

* Powerful out of the box with RESTful routes, plugins, sessions, signed
  cookies, static file server, testing framework, Perl-ish templates, JSON,
  I18N, first class Unicode support and much more for you to discover!

Duct Tape For The HTML5 Web
---------------------------

Web development for humans, making hard things possible and everything fun.

    use Mojolicious::Lite;

    get '/hello' => sub { shift->render(text => 'Hello World!') }

    get '/time' => 'clock';

    websocket '/echo' => sub {
        my $self = shift;
        $self->receive_message(
            sub {
                my ($self, $message) = @_;
                $self->send_message("echo: $message");
            }
        );
    };

    get '/fetch' => sub {
        my $self = shift;
        $self->render(
            data => $self->client->get('http://kraih.com')->res->body
        );
    };

    post '/:offset' => sub {
        my $self = shift;
        my $offset = $self->param('offset') || 23;
        $self->render(json => {list => [0 .. $offset]});
    };

    app->start;
    __DATA__

    @@ clock.html.ep
    % my ($second, $minute, $hour) = (localtime(time))[0, 1, 2];
    The time is <%= $hour %>:<%= $minute %>:<%= $second %>.

For more user friendly documentation see "perldoc Mojolicious::Guides"
and "perldoc Mojolicious::Lite".

Have Some Cake
--------------

    .---------------------------------------------------------------.
    |                             Fun!                              |
    '---------------------------------------------------------------'
    .---------------------------------------------------------------.
    |                                                               |
    |                .----------------------------------------------'
    |                | .--------------------------------------------.
    |   Application  | |              Mojolicious::Lite             |
    |                | '--------------------------------------------'
    |                | .--------------------------------------------.
    |                | |                 Mojolicious                |
    '----------------' '--------------------------------------------'
    .---------------------------------------------------------------.
    |                             Mojo                              |
    '---------------------------------------------------------------'
    .-------. .-----------. .--------. .------------. .-------------.
    |  CGI  | |  FastCGI  | |  PSGI  | |  HTTP 1.1  | |  WebSocket  |
    '-------' '-----------' '--------' '------------' '-------------'

To install this module type the following
-----------------------------------------

    perl Makefile.PL
    make
    make test
    make install