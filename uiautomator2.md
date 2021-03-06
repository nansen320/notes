Help on package uiautomator2:

NAME
    uiautomator2 - ::Timeout

DESCRIPTION
    atx-agent:ReverseProxy use http.DefaultTransport. Default Timeout: 30s
    
    |-- Dial --|-- TLS handshake --|-- Request --|-- Resp.headers --|-- Respose.body --|
    |------------------------------ http.Client.Timeout -------------------------------|
    
    Refs:
        - https://golang.org/pkg/net/http/#RoundTripper
        - http://colobu.com/2016/07/01/the-complete-guide-to-golang-net-http-timeouts

PACKAGE CONTENTS
    __main__
    abcd
    exceptions
    ext (package)
    image
    init
    messagebox
    session
    settings
    swipe
    utils
    version
    watcher
    webview
    widget
    xpath

CLASSES
    builtins.object
        AdbShell
        Device
    requests.sessions.Session(requests.sessions.SessionRedirectMixin)
        TimeoutRequestsSession
    
    class AdbShell(builtins.object)
     |  AdbShell(shellfn)
     |  
     |  Methods defined here:
     |  
     |  __init__(self, shellfn)
     |      Args:
     |          shellfn: Shell function
     |  
     |  is_screen_on(self)
     |  
     |  keyevent(self, v)
     |      Args:
     |          v: eg home wakeup back
     |  
     |  swipe(self, x0, y0, x1, y1)
     |  
     |  wmsize(self)
     |      get window size
     |      Returns:
     |          (width, height)
     |  
     |  ----------------------------------------------------------------------
     |  Data descriptors defined here:
     |  
     |  __dict__
     |      dictionary for instance variables (if defined)
     |  
     |  __weakref__
     |      list of weak references to the object (if defined)
    
    class Device(builtins.object)
     |  Device(host, port=7912)
     |  
     |  Methods defined here:
     |  
     |  __call__(self, **kwargs) -> uiautomator2.session.Session
     |      Call self as a function.
     |  
     |  __getattr__(self, attr)
     |  
     |  __init__(self, host, port=7912)
     |      Args:
     |          host (str): host address
     |          port (int): port number
     |      
     |      Raises:
     |          EnvironmentError
     |  
     |  __repr__(self)
     |      Return repr(self).
     |  
     |  __setattr__(self, key, value)
     |      Prevent creating new attributes outside __init__
     |  
     |  __str__(self)
     |      Return str(self).
     |  
     |  adb_shell(self, *args)
     |      Example:
     |          adb_shell('pwd')
     |          adb_shell('ls', '-l')
     |          adb_shell('ls -l')
     |      
     |      Returns:
     |          string for stdout merged with stderr, after the entire shell command is completed.
     |  
     |  app_clear(self, pkg_name)
     |      Stop and clear app data: pm clear
     |  
     |  app_current(self)
     |      Returns:
     |          dict(package, activity, pid?)
     |      
     |      Raises:
     |          EnvironementError
     |      
     |      For developer:
     |          Function reset_uiautomator need this function, so can't use jsonrpc here.
     |  
     |  app_icon(self, pkg_name)
     |      Returns:
     |          PIL.Image
     |      
     |      Raises:
     |          UiaError
     |  
     |  app_info(self, pkg_name)
     |      Get app info
     |      
     |      Args:
     |          pkg_name (str): package name
     |      
     |      Return example:
     |          {
     |              "mainActivity": "com.github.uiautomator.MainActivity",
     |              "label": "ATX",
     |              "versionName": "1.1.7",
     |              "versionCode": 1001007,
     |              "size":1760809
     |          }
     |      
     |      Raises:
     |          UiaError
     |  
     |  app_install(self, url, installing_callback=None, server=None)
     |      {u'message': u'downloading', "progress": {u'totalSize': 407992690, u'copiedSize': 49152}}
     |      
     |      Returns:
     |          packageName
     |      
     |      Raises:
     |          RuntimeError
     |  
     |  app_list(self, filter: str = None) -> list
     |      Args:
     |          filter: [-f] [-d] [-e] [-s] [-3] [-i] [-u] [--user USER_ID] [FILTER]
     |      Returns:
     |          list of apps by filter
     |  
     |  app_list_running(self) -> list
     |      Returns:
     |          list of running apps
     |  
     |  app_start(self, package_name, activity=None, extras={}, wait=False, stop=False, unlock=False, launch_timeout=None, use_monkey=False)
     |      Launch application
     |      Args:
     |          package_name (str): package name
     |          activity (str): app activity
     |          stop (bool): Stop app before starting the activity. (require activity)
     |          use_monkey (bool): use monkey command to start app when activity is not given
     |          wait (bool): wait until app started. default False
     |      
     |      Raises:
     |          SessionBrokenError
     |  
     |  app_stop(self, pkg_name)
     |      Stop one application: am force-stop
     |  
     |  app_stop_all(self, excludes=[])
     |      Stop all third party applications
     |      Args:
     |          excludes (list): apps that do now want to kill
     |      
     |      Returns:
     |          a list of killed apps
     |  
     |  app_uninstall(self, pkg_name) -> bool
     |      Uninstall an app 
     |      
     |      Returns:
     |          bool: success
     |  
     |  app_uninstall_all(self, excludes=[], verbose=False)
     |      Uninstall all apps
     |  
     |  app_wait(self, package_name: str, timeout: float = 20.0, front=False) -> int
     |      Wait until app launched
     |      Args:
     |          package_name (str): package name
     |          timeout (float): maxium wait time
     |          front (bool): wait until app is current app
     |      
     |      Returns:
     |          pid (int) 0 if launch failed
     |  
     |  current_app(self)
     |  
     |  disable_popups(self, enable=True)
     |      Automatic click all popups
     |      TODO: need fix
     |  
     |  healthcheck(self)
     |      Reset device into health state
     |      
     |      Raises:
     |          RuntimeError
     |  
     |  hooks_apply(self, stage, func_name, args=(), kwargs={}, ret=None)
     |      Args:
     |          stage(str): one of "before" or "after"
     |  
     |  hooks_register(self, func)
     |      Args:
     |          func: should accept 3 args. func_name:string, args:tuple, kwargs:dict
     |  
     |  jsonrpc_call(self, jsonrpc_url, method, params=[], http_timeout=60)
     |      jsonrpc2 call
     |      Refs:
     |          - http://www.jsonrpc.org/specification
     |  
     |  jsonrpc_retry_call(self, *args, **kwargs)
     |  
     |  open_identify(self, theme='black')
     |      Args:
     |          theme (str): black or red
     |  
     |  path2url(self, path)
     |  
     |  pull(self, src: str, dst: str)
     |      Pull file from device to local
     |      
     |      Raises:
     |          FileNotFoundError(py3) OSError(py2)
     |      
     |      Require atx-agent >= 0.0.9
     |  
     |  pull_content(self, src: str) -> bytes
     |      Read remote file content
     |      
     |      Raises:
     |          FileNotFoundError
     |  
     |  push(self, src, dst, mode=420)
     |      Args:
     |          src (path or fileobj): source file
     |          dst (str): destination can be folder or file path
     |      
     |      Returns:
     |          dict object, for example:
     |      
     |              {"mode": "0660", "size": 63, "target": "/sdcard/ABOUT.rst"}
     |      
     |          Since chmod may fail in android, the result "mode" may not same with input args(mode)
     |      
     |      Raises:
     |          IOError(if push got something wrong)
     |  
     |  push_url(self, url, dst, mode=420)
     |      Args:
     |          url (str): http url address
     |          dst (str): destination
     |          mode (str): file mode
     |      
     |      Raises:
     |          FileNotFoundError(py3) OSError(py2)
     |  
     |  request_agent(self, relative_url: str, method='get', timeout=60.0)
     |      send http-request to atx-agent
     |  
     |  reset_uiautomator(self, reason='unknown')
     |      Reset uiautomator
     |      
     |      Raises:
     |          RuntimeError
     |      
     |      Orders:
     |          - stop uiautomator keeper
     |          - am force-stop com.github.uiautomator
     |          - start uiautomator keeper(am instrument -w ...)
     |          - wait until uiautomator service is ready
     |  
     |  screenshot(self, *args, **kwargs)
     |      Take screenshot of device
     |      
     |      Returns:
     |          PIL.Image
     |  
     |  service(self, name)
     |      Manage service start or stop
     |      
     |      Example:
     |          d.service("uiautomator").start()
     |          d.service("uiautomator").stop()
     |  
     |  session(self, pkg_name=None, attach=False, launch_timeout=None, strict=False)
     |      Create a new session
     |      
     |      Args:
     |          pkg_name (str): android package name
     |          attach (bool): attach to already running app
     |          launch_timeout (int): launch timeout
     |          strict (bool): used along with attach, 
     |              when attach and strict both true, SessionBrokenError will raise if app not running
     |      
     |      Raises:
     |          requests.HTTPError, SessionBrokenError
     |  
     |  set_new_command_timeout(self, timeout: int)
     |      default 3 minutes
     |      Args:
     |          timeout (int): seconds
     |  
     |  setup_jsonrpc(self, jsonrpc_url=None)
     |      Wrap jsonrpc call into object
     |      Usage example:
     |          self.setup_jsonrpc().pressKey("home")
     |  
     |  shell(self, cmdargs, stream=False, timeout=60)
     |      Run adb shell command with arguments and return its output. Require atx-agent >=0.3.3
     |      
     |      Args:
     |          cmdargs: str or list, example: "ls -l" or ["ls", "-l"]
     |          timeout: seconds of command run, works on when stream is False
     |          stream: bool used for long running process.
     |      
     |      Returns:
     |          (output, exit_code) when stream is False
     |          requests.Response when stream is True, you have to close it after using
     |      
     |      Raises:
     |          RuntimeError
     |      
     |      For atx-agent is not support return exit code now.
     |      When command got something wrong, exit_code is always 1, otherwise exit_code is always 0
     |  
     |  unlock(self)
     |      unlock screen
     |  
     |  wait_activity(self, activity, timeout=10)
     |      wait activity
     |      Args:
     |          activity (str): name of activity
     |          timeout (float): max wait time
     |      
     |      Returns:
     |          bool of activity
     |  
     |  window_size(self)
     |      return (width, height)
     |  
     |  ----------------------------------------------------------------------
     |  Static methods defined here:
     |  
     |  plugins()
     |  
     |  ----------------------------------------------------------------------
     |  Readonly properties defined here:
     |  
     |  address
     |  
     |  agent_alive
     |  
     |  alive
     |  
     |  device_info
     |  
     |  image
     |  
     |  jsonrpc
     |      Make jsonrpc call easier
     |      For example:
     |          self.jsonrpc.pressKey("home")
     |  
     |  screenshot_uri
     |  
     |  serial
     |  
     |  settings
     |  
     |  taobao
     |  
     |  uiautomator
     |  
     |  watcher
     |  
     |  wlan_ip
     |  
     |  xpath
     |  
     |  ----------------------------------------------------------------------
     |  Data descriptors defined here:
     |  
     |  __dict__
     |      dictionary for instance variables (if defined)
     |  
     |  __weakref__
     |      list of weak references to the object (if defined)
     |  
     |  click_post_delay
     |  
     |  debug
     |  
     |  wait_timeout
    
    class TimeoutRequestsSession(requests.sessions.Session)
     |  A Requests session.
     |  
     |  Provides cookie persistence, connection-pooling, and configuration.
     |  
     |  Basic Usage::
     |  
     |    >>> import requests
     |    >>> s = requests.Session()
     |    >>> s.get('https://httpbin.org/get')
     |    <Response [200]>
     |  
     |  Or as a context manager::
     |  
     |    >>> with requests.Session() as s:
     |    >>>     s.get('https://httpbin.org/get')
     |    <Response [200]>
     |  
     |  Method resolution order:
     |      TimeoutRequestsSession
     |      requests.sessions.Session
     |      requests.sessions.SessionRedirectMixin
     |      builtins.object
     |  
     |  Methods defined here:
     |  
     |  __init__(self)
     |      Initialize self.  See help(type(self)) for accurate signature.
     |  
     |  request(self, method, url, **kwargs)
     |      Constructs a :class:`Request <Request>`, prepares it and sends it.
     |      Returns :class:`Response <Response>` object.
     |      
     |      :param method: method for the new :class:`Request` object.
     |      :param url: URL for the new :class:`Request` object.
     |      :param params: (optional) Dictionary or bytes to be sent in the query
     |          string for the :class:`Request`.
     |      :param data: (optional) Dictionary, list of tuples, bytes, or file-like
     |          object to send in the body of the :class:`Request`.
     |      :param json: (optional) json to send in the body of the
     |          :class:`Request`.
     |      :param headers: (optional) Dictionary of HTTP Headers to send with the
     |          :class:`Request`.
     |      :param cookies: (optional) Dict or CookieJar object to send with the
     |          :class:`Request`.
     |      :param files: (optional) Dictionary of ``'filename': file-like-objects``
     |          for multipart encoding upload.
     |      :param auth: (optional) Auth tuple or callable to enable
     |          Basic/Digest/Custom HTTP Auth.
     |      :param timeout: (optional) How long to wait for the server to send
     |          data before giving up, as a float, or a :ref:`(connect timeout,
     |          read timeout) <timeouts>` tuple.
     |      :type timeout: float or tuple
     |      :param allow_redirects: (optional) Set to True by default.
     |      :type allow_redirects: bool
     |      :param proxies: (optional) Dictionary mapping protocol or protocol and
     |          hostname to the URL of the proxy.
     |      :param stream: (optional) whether to immediately download the response
     |          content. Defaults to ``False``.
     |      :param verify: (optional) Either a boolean, in which case it controls whether we verify
     |          the server's TLS certificate, or a string, in which case it must be a path
     |          to a CA bundle to use. Defaults to ``True``.
     |      :param cert: (optional) if String, path to ssl client cert file (.pem).
     |          If Tuple, ('cert', 'key') pair.
     |      :rtype: requests.Response
     |  
     |  ----------------------------------------------------------------------
     |  Methods inherited from requests.sessions.Session:
     |  
     |  __enter__(self)
     |  
     |  __exit__(self, *args)
     |  
     |  __getstate__(self)
     |  
     |  __setstate__(self, state)
     |  
     |  close(self)
     |      Closes all adapters and as such the session
     |  
     |  delete(self, url, **kwargs)
     |      Sends a DELETE request. Returns :class:`Response` object.
     |      
     |      :param url: URL for the new :class:`Request` object.
     |      :param \*\*kwargs: Optional arguments that ``request`` takes.
     |      :rtype: requests.Response
     |  
     |  get(self, url, **kwargs)
     |      Sends a GET request. Returns :class:`Response` object.
     |      
     |      :param url: URL for the new :class:`Request` object.
     |      :param \*\*kwargs: Optional arguments that ``request`` takes.
     |      :rtype: requests.Response
     |  
     |  get_adapter(self, url)
     |      Returns the appropriate connection adapter for the given URL.
     |      
     |      :rtype: requests.adapters.BaseAdapter
     |  
     |  head(self, url, **kwargs)
     |      Sends a HEAD request. Returns :class:`Response` object.
     |      
     |      :param url: URL for the new :class:`Request` object.
     |      :param \*\*kwargs: Optional arguments that ``request`` takes.
     |      :rtype: requests.Response
     |  
     |  merge_environment_settings(self, url, proxies, stream, verify, cert)
     |      Check the environment and merge it with some settings.
     |      
     |      :rtype: dict
     |  
     |  mount(self, prefix, adapter)
     |      Registers a connection adapter to a prefix.
     |      
     |      Adapters are sorted in descending order by prefix length.
     |  
     |  options(self, url, **kwargs)
     |      Sends a OPTIONS request. Returns :class:`Response` object.
     |      
     |      :param url: URL for the new :class:`Request` object.
     |      :param \*\*kwargs: Optional arguments that ``request`` takes.
     |      :rtype: requests.Response
     |  
     |  patch(self, url, data=None, **kwargs)
     |      Sends a PATCH request. Returns :class:`Response` object.
     |      
     |      :param url: URL for the new :class:`Request` object.
     |      :param data: (optional) Dictionary, list of tuples, bytes, or file-like
     |          object to send in the body of the :class:`Request`.
     |      :param \*\*kwargs: Optional arguments that ``request`` takes.
     |      :rtype: requests.Response
     |  
     |  post(self, url, data=None, json=None, **kwargs)
     |      Sends a POST request. Returns :class:`Response` object.
     |      
     |      :param url: URL for the new :class:`Request` object.
     |      :param data: (optional) Dictionary, list of tuples, bytes, or file-like
     |          object to send in the body of the :class:`Request`.
     |      :param json: (optional) json to send in the body of the :class:`Request`.
     |      :param \*\*kwargs: Optional arguments that ``request`` takes.
     |      :rtype: requests.Response
     |  
     |  prepare_request(self, request)
     |      Constructs a :class:`PreparedRequest <PreparedRequest>` for
     |      transmission and returns it. The :class:`PreparedRequest` has settings
     |      merged from the :class:`Request <Request>` instance and those of the
     |      :class:`Session`.
     |      
     |      :param request: :class:`Request` instance to prepare with this
     |          session's settings.
     |      :rtype: requests.PreparedRequest
     |  
     |  put(self, url, data=None, **kwargs)
     |      Sends a PUT request. Returns :class:`Response` object.
     |      
     |      :param url: URL for the new :class:`Request` object.
     |      :param data: (optional) Dictionary, list of tuples, bytes, or file-like
     |          object to send in the body of the :class:`Request`.
     |      :param \*\*kwargs: Optional arguments that ``request`` takes.
     |      :rtype: requests.Response
     |  
     |  send(self, request, **kwargs)
     |      Send a given PreparedRequest.
     |      
     |      :rtype: requests.Response
     |  
     |  ----------------------------------------------------------------------
     |  Data and other attributes inherited from requests.sessions.Session:
     |  
     |  __attrs__ = ['headers', 'cookies', 'auth', 'proxies', 'hooks', 'params...
     |  
     |  ----------------------------------------------------------------------
     |  Methods inherited from requests.sessions.SessionRedirectMixin:
     |  
     |  get_redirect_target(self, resp)
     |      Receives a Response. Returns a redirect URI or ``None``
     |  
     |  rebuild_auth(self, prepared_request, response)
     |      When being redirected we may want to strip authentication from the
     |      request to avoid leaking credentials. This method intelligently removes
     |      and reapplies authentication where possible to avoid credential loss.
     |  
     |  rebuild_method(self, prepared_request, response)
     |      When being redirected we may want to change the method of the request
     |      based on certain specs or browser behavior.
     |  
     |  rebuild_proxies(self, prepared_request, proxies)
     |      This method re-evaluates the proxy configuration by considering the
     |      environment variables. If we are redirected to a URL covered by
     |      NO_PROXY, we strip the proxy configuration. Otherwise, we set missing
     |      proxy keys for this URL (in case they were stripped by a previous
     |      redirect).
     |      
     |      This method also replaces the Proxy-Authorization header where
     |      necessary.
     |      
     |      :rtype: dict
     |  
     |  resolve_redirects(self, resp, req, stream=False, timeout=None, verify=True, cert=None, proxies=None, yield_requests=False, **adapter_kwargs)
     |      Receives a Response. Returns a generator of Responses or Requests.
     |  
     |  should_strip_auth(self, old_url, new_url)
     |      Decide whether Authorization header should be removed when redirecting
     |  
     |  ----------------------------------------------------------------------
     |  Data descriptors inherited from requests.sessions.SessionRedirectMixin:
     |  
     |  __dict__
     |      dictionary for instance variables (if defined)
     |  
     |  __weakref__
     |      list of weak references to the object (if defined)
    
    UIAutomatorServer = class Device(builtins.object)
     |  UIAutomatorServer(host, port=7912)
     |  
     |  Methods defined here:
     |  
     |  __call__(self, **kwargs) -> uiautomator2.session.Session
     |      Call self as a function.
     |  
     |  __getattr__(self, attr)
     |  
     |  __init__(self, host, port=7912)
     |      Args:
     |          host (str): host address
     |          port (int): port number
     |      
     |      Raises:
     |          EnvironmentError
     |  
     |  __repr__(self)
     |      Return repr(self).
     |  
     |  __setattr__(self, key, value)
     |      Prevent creating new attributes outside __init__
     |  
     |  __str__(self)
     |      Return str(self).
     |  
     |  adb_shell(self, *args)
     |      Example:
     |          adb_shell('pwd')
     |          adb_shell('ls', '-l')
     |          adb_shell('ls -l')
     |      
     |      Returns:
     |          string for stdout merged with stderr, after the entire shell command is completed.
     |  
     |  app_clear(self, pkg_name)
     |      Stop and clear app data: pm clear
     |  
     |  app_current(self)
     |      Returns:
     |          dict(package, activity, pid?)
     |      
     |      Raises:
     |          EnvironementError
     |      
     |      For developer:
     |          Function reset_uiautomator need this function, so can't use jsonrpc here.
     |  
     |  app_icon(self, pkg_name)
     |      Returns:
     |          PIL.Image
     |      
     |      Raises:
     |          UiaError
     |  
     |  app_info(self, pkg_name)
     |      Get app info
     |      
     |      Args:
     |          pkg_name (str): package name
     |      
     |      Return example:
     |          {
     |              "mainActivity": "com.github.uiautomator.MainActivity",
     |              "label": "ATX",
     |              "versionName": "1.1.7",
     |              "versionCode": 1001007,
     |              "size":1760809
     |          }
     |      
     |      Raises:
     |          UiaError
     |  
     |  app_install(self, url, installing_callback=None, server=None)
     |      {u'message': u'downloading', "progress": {u'totalSize': 407992690, u'copiedSize': 49152}}
     |      
     |      Returns:
     |          packageName
     |      
     |      Raises:
     |          RuntimeError
     |  
     |  app_list(self, filter: str = None) -> list
     |      Args:
     |          filter: [-f] [-d] [-e] [-s] [-3] [-i] [-u] [--user USER_ID] [FILTER]
     |      Returns:
     |          list of apps by filter
     |  
     |  app_list_running(self) -> list
     |      Returns:
     |          list of running apps
     |  
     |  app_start(self, package_name, activity=None, extras={}, wait=False, stop=False, unlock=False, launch_timeout=None, use_monkey=False)
     |      Launch application
     |      Args:
     |          package_name (str): package name
     |          activity (str): app activity
     |          stop (bool): Stop app before starting the activity. (require activity)
     |          use_monkey (bool): use monkey command to start app when activity is not given
     |          wait (bool): wait until app started. default False
     |      
     |      Raises:
     |          SessionBrokenError
     |  
     |  app_stop(self, pkg_name)
     |      Stop one application: am force-stop
     |  
     |  app_stop_all(self, excludes=[])
     |      Stop all third party applications
     |      Args:
     |          excludes (list): apps that do now want to kill
     |      
     |      Returns:
     |          a list of killed apps
     |  
     |  app_uninstall(self, pkg_name) -> bool
     |      Uninstall an app 
     |      
     |      Returns:
     |          bool: success
     |  
     |  app_uninstall_all(self, excludes=[], verbose=False)
     |      Uninstall all apps
     |  
     |  app_wait(self, package_name: str, timeout: float = 20.0, front=False) -> int
     |      Wait until app launched
     |      Args:
     |          package_name (str): package name
     |          timeout (float): maxium wait time
     |          front (bool): wait until app is current app
     |      
     |      Returns:
     |          pid (int) 0 if launch failed
     |  
     |  current_app(self)
     |  
     |  disable_popups(self, enable=True)
     |      Automatic click all popups
     |      TODO: need fix
     |  
     |  healthcheck(self)
     |      Reset device into health state
     |      
     |      Raises:
     |          RuntimeError
     |  
     |  hooks_apply(self, stage, func_name, args=(), kwargs={}, ret=None)
     |      Args:
     |          stage(str): one of "before" or "after"
     |  
     |  hooks_register(self, func)
     |      Args:
     |          func: should accept 3 args. func_name:string, args:tuple, kwargs:dict
     |  
     |  jsonrpc_call(self, jsonrpc_url, method, params=[], http_timeout=60)
     |      jsonrpc2 call
     |      Refs:
     |          - http://www.jsonrpc.org/specification
     |  
     |  jsonrpc_retry_call(self, *args, **kwargs)
     |  
     |  open_identify(self, theme='black')
     |      Args:
     |          theme (str): black or red
     |  
     |  path2url(self, path)
     |  
     |  pull(self, src: str, dst: str)
     |      Pull file from device to local
     |      
     |      Raises:
     |          FileNotFoundError(py3) OSError(py2)
     |      
     |      Require atx-agent >= 0.0.9
     |  
     |  pull_content(self, src: str) -> bytes
     |      Read remote file content
     |      
     |      Raises:
     |          FileNotFoundError
     |  
     |  push(self, src, dst, mode=420)
     |      Args:
     |          src (path or fileobj): source file
     |          dst (str): destination can be folder or file path
     |      
     |      Returns:
     |          dict object, for example:
     |      
     |              {"mode": "0660", "size": 63, "target": "/sdcard/ABOUT.rst"}
     |      
     |          Since chmod may fail in android, the result "mode" may not same with input args(mode)
     |      
     |      Raises:
     |          IOError(if push got something wrong)
     |  
     |  push_url(self, url, dst, mode=420)
     |      Args:
     |          url (str): http url address
     |          dst (str): destination
     |          mode (str): file mode
     |      
     |      Raises:
     |          FileNotFoundError(py3) OSError(py2)
     |  
     |  request_agent(self, relative_url: str, method='get', timeout=60.0)
     |      send http-request to atx-agent
     |  
     |  reset_uiautomator(self, reason='unknown')
     |      Reset uiautomator
     |      
     |      Raises:
     |          RuntimeError
     |      
     |      Orders:
     |          - stop uiautomator keeper
     |          - am force-stop com.github.uiautomator
     |          - start uiautomator keeper(am instrument -w ...)
     |          - wait until uiautomator service is ready
     |  
     |  screenshot(self, *args, **kwargs)
     |      Take screenshot of device
     |      
     |      Returns:
     |          PIL.Image
     |  
     |  service(self, name)
     |      Manage service start or stop
     |      
     |      Example:
     |          d.service("uiautomator").start()
     |          d.service("uiautomator").stop()
     |  
     |  session(self, pkg_name=None, attach=False, launch_timeout=None, strict=False)
     |      Create a new session
     |      
     |      Args:
     |          pkg_name (str): android package name
     |          attach (bool): attach to already running app
     |          launch_timeout (int): launch timeout
     |          strict (bool): used along with attach, 
     |              when attach and strict both true, SessionBrokenError will raise if app not running
     |      
     |      Raises:
     |          requests.HTTPError, SessionBrokenError
     |  
     |  set_new_command_timeout(self, timeout: int)
     |      default 3 minutes
     |      Args:
     |          timeout (int): seconds
     |  
     |  setup_jsonrpc(self, jsonrpc_url=None)
     |      Wrap jsonrpc call into object
     |      Usage example:
     |          self.setup_jsonrpc().pressKey("home")
     |  
     |  shell(self, cmdargs, stream=False, timeout=60)
     |      Run adb shell command with arguments and return its output. Require atx-agent >=0.3.3
     |      
     |      Args:
     |          cmdargs: str or list, example: "ls -l" or ["ls", "-l"]
     |          timeout: seconds of command run, works on when stream is False
     |          stream: bool used for long running process.
     |      
     |      Returns:
     |          (output, exit_code) when stream is False
     |          requests.Response when stream is True, you have to close it after using
     |      
     |      Raises:
     |          RuntimeError
     |      
     |      For atx-agent is not support return exit code now.
     |      When command got something wrong, exit_code is always 1, otherwise exit_code is always 0
     |  
     |  unlock(self)
     |      unlock screen
     |  
     |  wait_activity(self, activity, timeout=10)
     |      wait activity
     |      Args:
     |          activity (str): name of activity
     |          timeout (float): max wait time
     |      
     |      Returns:
     |          bool of activity
     |  
     |  window_size(self)
     |      return (width, height)
     |  
     |  ----------------------------------------------------------------------
     |  Static methods defined here:
     |  
     |  plugins()
     |  
     |  ----------------------------------------------------------------------
     |  Readonly properties defined here:
     |  
     |  address
     |  
     |  agent_alive
     |  
     |  alive
     |  
     |  device_info
     |  
     |  image
     |  
     |  jsonrpc
     |      Make jsonrpc call easier
     |      For example:
     |          self.jsonrpc.pressKey("home")
     |  
     |  screenshot_uri
     |  
     |  serial
     |  
     |  settings
     |  
     |  taobao
     |  
     |  uiautomator
     |  
     |  watcher
     |  
     |  wlan_ip
     |  
     |  xpath
     |  
     |  ----------------------------------------------------------------------
     |  Data descriptors defined here:
     |  
     |  __dict__
     |      dictionary for instance variables (if defined)
     |  
     |  __weakref__
     |      list of weak references to the object (if defined)
     |  
     |  click_post_delay
     |  
     |  debug
     |  
     |  wait_timeout

FUNCTIONS
    connect(addr=None)
        Args:
            addr (str): uiautomator server address or serial number. default from env-var ANDROID_DEVICE_IP
        
        Returns:
            Device
        
        Raises:
            ConnectError
        
        Example:
            connect("10.0.0.1:7912")
            connect("10.0.0.1") # use default 7912 port
            connect("http://10.0.0.1")
            connect("http://10.0.0.1:7912")
            connect("cff1123ea")  # adb device serial number
    
    connect_adb_wifi(addr)
        Run adb connect, and then call connect_usb(..)
        
        Args:
            addr: ip+port which can be used for "adb connect" argument
        
        Raises:
            ConnectError
    
    connect_usb(serial=None, healthcheck=False, init=True)
        Args:
            serial (str): android device serial
            healthcheck (bool): start uiautomator if not ready
            init (bool): initial with apk and atx-agent
        
        Returns:
            Device
        
        Raises:
            ConnectError
    
    connect_wifi(addr: str) -> 'Device'
        Args:
            addr (str) uiautomator server address.
        
        Returns:
            Device
        
        Raises:
            ConnectError
        
        Examples:
            connect_wifi("10.0.0.1")
    
    fix_wifi_addr(addr: str) -> Union[str, NoneType]
    
    log_print(s)
    
    plugin_clear()
    
    plugin_register(name, plugin, *args, **kwargs)
        Add plugin into Device
        
        Args:
            name: string
            plugin: class or function which take d as first parameter
        
        Example:
            def upload_screenshot(d):
                def inner():
                    d.screenshot("tmp.jpg")
                    # use requests.post upload tmp.jpg
                return inner
        
            plugin_register("upload_screenshot", save_screenshot)
        
            d = u2.connect()
            d.ext_upload_screenshot()

DATA
    DEBUG = False
    HTTP_TIMEOUT = 60
    Optional = typing.Optional
    Union = typing.Union
    __atx_agent_version__ = '0.8.0'
    absolute_import = _Feature((2, 5, 0, 'alpha', 1), (3, 0, 0, 'alpha', 0...
    logger = <Logger logzero_default (DEBUG)>
    print_function = _Feature((2, 6, 0, 'alpha', 2), (3, 0, 0, 'alpha', 0)...

FILE
    /Library/Frameworks/Python.framework/Versions/3.8/lib/python3.8/site-packages/uiautomator2/__init__.py
