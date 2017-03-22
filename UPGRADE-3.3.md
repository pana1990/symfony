UPGRADE FROM 3.2 to 3.3
=======================

BrowserKit
----------

 * The request method is dropped from POST to GET when the response
   status code is 301.

ClassLoader
-----------

 * The component is deprecated and will be removed in 4.0. Use Composer instead.

Console
-------

* `Input::getOption()` no longer returns the default value for options
  with value optional explicitly passed empty.

  For:

  ```php
  protected function configure()
  {
      $this
          // ...
          ->setName('command')
          ->addOption('foo', null, InputOption::VALUE_OPTIONAL, '', 'default')
       ;
  }

  protected function execute(InputInterface $input, OutputInterface $output)
  {
      var_dump($input->getOption('foo'));
  }
  ```

  Before:

  ```
  $ php console.php command
  "default"

  $ php console.php command --foo
  "default"

  $ php console.php command --foo ""
  "default"

  $ php console.php command --foo=
  "default"
  ```

  After:

  ```
  $ php console.php command
  "default"

  $ php console.php command --foo
  NULL

  $ php console.php command --foo ""
  ""

  $ php console.php command --foo=
  ""
  ```

Debug
-----

 * The `ContextErrorException` class is deprecated. `\ErrorException` will be used instead in 4.0.

DependencyInjection
-------------------

 * Autowiring-types have been deprecated, use aliases instead.

   Before:

   ```xml
   <service id="annotations.reader" class="Doctrine\Common\Annotations\AnnotationReader" public="false">
       <autowiring-type>Doctrine\Common\Annotations\Reader</autowiring-type>
   </service>
   ```

   After:

   ```xml
   <service id="annotations.reader" class="Doctrine\Common\Annotations\AnnotationReader" public="false" />
   <service id="Doctrine\Common\Annotations\Reader" alias="annotations.reader" public="false" />
   ```

 * The `Reference` and `Alias` classes do not make service identifiers lowercase anymore.

 * Case insensitivity of service identifiers is deprecated and will be removed in 4.0.

 * Using the `PhpDumper` with an uncompiled `ContainerBuilder` is deprecated and
   will not be supported anymore in 4.0.

 * Extending the containers generated by `PhpDumper` is deprecated and won't be
   supported in 4.0.

 * The `DefinitionDecorator` class is deprecated and will be removed in 4.0, use
   the `ChildDefinition` class instead.

 * The ``strict`` attribute in service arguments has been deprecated and will be removed in 4.0.
   The attribute is ignored since 3.0, so you can simply remove it.

EventDispatcher
---------------

 * The `ContainerAwareEventDispatcher` class has been deprecated.
   Use `EventDispatcher` with closure-proxy injection instead.

Finder
------

 * The `ExceptionInterface` has been deprecated and will be removed in 4.0.

FrameworkBundle
---------------

 * The `cache:clear` command should always be called with the `--no-warmup` option.
   Warmup should be done via the `cache:warmup` command.

 * The "framework.trusted_proxies" configuration option and the corresponding "kernel.trusted_proxies" parameter have been deprecated and will be removed in 4.0. Use the Request::setTrustedProxies() method in your front controller instead.


 * The `Symfony\Bundle\FrameworkBundle\DependencyInjection\Compiler\AddConsoleCommandPass` has been deprecated. Use `Symfony\Component\Console\DependencyInjection\AddConsoleCommandPass` instead.

 * The `Symfony\Bundle\FrameworkBundle\DependencyInjection\Compiler\SerializerPass` class has been
   deprecated and will be removed in 4.0.
   Use the `Symfony\Component\Serializer\DependencyInjection\SerializerPass` class instead.

 * The `Symfony\Bundle\FrameworkBundle\DependencyInjection\Compiler\FormPass` class has been
   deprecated and will be removed in 4.0. Use the `Symfony\Component\Form\DependencyInjection\FormPass`
   class instead.

 * The `Symfony\Bundle\FrameworkBundle\EventListener\SessionListener` class has been
   deprecated and will be removed in 4.0. Use the `Symfony\Component\HttpKernel\EventListener\SessionListener`
   class instead.

 * The `Symfony\Bundle\FrameworkBundle\EventListener\TestSessionListener` class has been
   deprecated and will be removed in 4.0. Use the `Symfony\Component\HttpKernel\EventListener\TestSessionListener`
   class instead.

 * The `Symfony\Bundle\FrameworkBundle\DependencyInjection\Compiler\ConfigCachePass` class has been
   deprecated and will be removed in 4.0. Use `Symfony\Component\Config\DependencyInjection\ConfigCachePass`
   class instead.

 * The `Symfony\Bundle\FrameworkBundle\DependencyInjection\Compiler\PropertyInfoPass` class has been
   deprecated and will be removed in 4.0. Use the `Symfony\Component\PropertyInfo\DependencyInjection\PropertyInfoPass`
   class instead.

 * The `ConstraintValidatorFactory::$validators` and `$container` properties
   have been deprecated and will be removed in 4.0.

 * Extending `ConstraintValidatorFactory` is deprecated and won't be supported in 4.0.

 * Class parameters related to routing have been deprecated and will be removed in 4.0.
     * router.options.generator_class
     * router.options.generator_base_class
     * router.options.generator_dumper_class
     * router.options.matcher_class
     * router.options.matcher_base_class
     * router.options.matcher_dumper_class
     * router.options.matcher.cache_class
     * router.options.generator.cache_class

 * The `Symfony\Bundle\FrameworkBundle\DependencyInjection\Compiler\ControllerArgumentValueResolverPass` class
   has been deprecated and will be removed in 4.0. Use the `Symfony\Component\HttpKernel\DependencyInjection\ControllerArgumentValueResolverPass`
   class instead.

 * The `Symfony\Bundle\FrameworkBundle\DependencyInjection\Compiler\RoutingResolverPass`
   class has been deprecated and will be removed in 4.0. Use the
   `Symfony\Component\Routing\DependencyInjection\RoutingResolverPass` class instead.

 * The `server:run`, `server:start`, `server:stop` and
   `server:status` console commands have been moved to a dedicated bundle.
   Require `symfony/web-server-bundle` in your composer.json and register
   `Symfony\Bundle\WebServerBundle\WebServerBundle` in your AppKernel to use them.

 * The `Symfony\Bundle\FrameworkBundle\Translation\Translator` constructor now takes the
   default locale as 3rd argument. Not passing it will trigger an error in 4.0.

HttpFoundation
--------------

 * The `Request::setTrustedProxies()` method takes a new `$trustedHeaderSet` argument - not setting it is deprecated.
   Set it to `Request::HEADER_FORWARDED` if your reverse-proxy uses the RFC7239 `Forwarded` header,
   or to `Request::HEADER_X_FORWARDED_ALL` if it is using `X-Forwarded-*` headers instead.

 * The `Request::setTrustedHeaderName()` and `Request::getTrustedHeaderName()` methods are deprecated,
   use the RFC7239 `Forwarded` header, or the `X-Forwarded-*` headers instead.

HttpKernel
-----------

 * The `Psr6CacheClearer::addPool()` method has been deprecated. Pass an array
   of pools indexed by name to the constructor instead.

 * The `LazyLoadingFragmentHandler::addRendererService()` method has been
   deprecated and will be removed in 4.0.

 * The `X-Status-Code` header method of setting a custom status code in the
   response when handling exceptions has been removed. There is now a new
   `GetResponseForExceptionEvent::allowCustomResponseCode()` method instead,
   which will tell the Kernel to use the response code set on the event's
   response object.

 * The `Kernel::getEnvParameters()` method has been deprecated and will be
   removed in 4.0.

 * The `SYMFONY__` environment variables have been deprecated and they will be
   no longer processed automatically by Symfony in 4.0. Use the `%env()%` syntax
   to get the value of any environment variable from configuration files instead.

Process
-------

 * The `ProcessUtils::escapeArgument()` method has been deprecated, use a command line array or give env vars to the `Process::start/run()` method instead.

 * Not inheriting environment variables is deprecated.

 * Configuring `proc_open()` options is deprecated.

 * Configuring Windows and sigchild compatibility is deprecated - they will be always enabled in 4.0.

 * Extending `Process::run()`, `Process::mustRun()` and `Process::restart()` is
   deprecated and won't be supported in 4.0.

Security
--------

 * The `RoleInterface` has been deprecated. Extend the `Symfony\Component\Security\Core\Role\Role`
   class in your custom role implementations instead.

SecurityBundle
--------------

 * The `FirewallContext::getContext()` method has been deprecated and will be removed in 4.0.
   Use the `getListeners()` method instead.

 * The `FirewallMap::$map` and `$container` properties have been deprecated and will be removed in 4.0.

 * The `UserPasswordEncoderCommand` command expects to be registered as a service and its
   constructor arguments fully provided.
   Registering by convention the command or commands extending it is deprecated and will
   not be allowed anymore in 4.0.

 * `UserPasswordEncoderCommand::getContainer()` is deprecated, and this class won't
    extend `ContainerAwareCommand` nor implement `ContainerAwareInterface` anymore in 4.0.

 * [BC BREAK] Keys of the `users` node for `in_memory` user provider are no longer normalized.

Serializer
----------

 * Extending `ChainDecoder`, `ChainEncoder`, `ArrayDenormalizer` is deprecated
   and won't be supported in 4.0.

TwigBridge
----------

 * The `TwigRendererEngine::setEnvironment()` method has been deprecated and will be removed
   in 4.0. Pass the Twig Environment as second argument of the constructor instead.

TwigBundle
----------

* The `ContainerAwareRuntimeLoader` class has been deprecated and will be removed in 4.0.
  Use the Twig `Twig_ContainerRuntimeLoader` class instead.

Workflow
--------

 * Deprecated class name support in `WorkflowRegistry::add()` as second parameter.
   Wrap the class name in an instance of ClassInstanceSupportStrategy instead.

Yaml
----

 * Starting an unquoted string with a question mark followed by a space is
   deprecated and will throw a `ParseException` in Symfony 4.0.

 * Deprecated support for implicitly parsing non-string mapping keys as strings.
   Mapping keys that are no strings will lead to a `ParseException` in Symfony
   4.0. Use the `PARSE_KEYS_AS_STRINGS` flag to opt-in for keys to be parsed as
   strings.

   Before:

   ```php
   $yaml = <<<YAML
   null: null key
   true: boolean true
   1: integer key
   2.0: float key
   YAML;

   Yaml::parse($yaml);
   ```

   After:

   ```php

   $yaml = <<<YAML
   null: null key
   true: boolean true
   1: integer key
   2.0: float key
   YAML;

   Yaml::parse($yaml, Yaml::PARSE_KEYS_AS_STRINGS);
   ```

 * Omitting the key of a mapping is deprecated and will throw a `ParseException` in Symfony 4.0.

 * The constructor arguments `$offset`, `$totalNumberOfLines` and
   `$skippedLineNumbers` of the `Parser` class are deprecated and will be
   removed in 4.0