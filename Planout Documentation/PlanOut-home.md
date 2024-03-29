PlanOut
=======

A framework for online field experiments

* [Get Started](/web/20200928084631/http://facebook.github.io/planout/docs/getting-started.html)
* [GitHub](https://web.archive.org/web/20200928084631/http://github.com/facebook/planout)

### Focus on parameters

PlanOut provides randomized parameter values to Internet services. Instead of using constants for user interface elements or switches controlling the rollout of a new feature or ranking model, just use PlanOut to determine the value of these parameters. Now you have an experiment.

### Simple or complex

It is easy to implement simple A/B tests in PlanOut. But it's also not much harder to implement factorial or within-subjects designs, or more complex designs involving multiple types of units (e.g., users and content), and conditional logic. Easily run experiments that help you understand your product and answer important questions.

### Extensible

PlanOut was developed at Facebook for running experiments involving hundreds of millions of people. It has been written with portability and extensibility in mind, and has been ported to all major Web programming languages, including Python, Java, PHP, JavaScript, Ruby, and Go.

PlanOut is a framework for online field experiments. It was created to make it easy to run and iterate on sophisticated experiments in a statistically sound manner while satisfying the constraints of deployed Internet services.

Developers implement experiments using PlanOut by providing a high-level specification for how _units_ (e.g., users, cookie IDs) should be mapped to parameters that control the user experience. For example, to create a 2x2 factorial experiment that randomizes both the color and the text on a button, using the Python-based framework, one can simply create a class like this:

    class MyExperiment(SimpleExperiment):
      def assign(self, params, userid):
        params.button_color = UniformChoice(choices=['#ff0000', '#00ff00'],
          unit=userid)
        params.button_text = UniformChoice(choices=['I voted', 'I am a voter'],
          unit=userid)
    

Then, in the application code, instead of just using a constant (e.g., ‘#ff00000’), you query an instance of the class to find out what values should be used for the current user:

    my_exp = MyExperiment(userid=42)
    color = my_exp.get('button_color')
    text = my_exp.get('button_text')
    

PlanOut takes care of correctly randomizing each `userid` to parameter values. It does so by deterministically hashing the input, so each `userid` will always map onto the same parameter values for that experiment. As soon as you access any of the parameters, core parts of the data you need to analyze your experiment are automatically logged.

The PlanOut framework includes:

*   Extensible classes for [implementing](docs/getting-started.html) and [testing](docs/testing.html) experiments, which [automatically log](docs/logging.html) important data.
    
*   A system for managing and deploying multiple mutually exclusive experiments, called [namespaces](docs/namespaces.html)
    
*   The [PlanOut language](docs/planout-language.html), which lets you define, serialize, store, and execute experiment definitions in a platform-independent way.
    

### Who is PlanOut for?

PlanOut is for researchers, businesses, and students wanting to run experiments. It’s designed to be easy to get up and running with for first-time experimenters, and extensible for those wanting to use it in a large production environments. This open source implementation shares many of the key design decisions of Facebook’s experimentation stack, which is used to conduct experiments with hundreds of millions of people.

### Learn more

Continue on to the [documentation page](docs/getting-started.html) or try out the interactive [PlanOut editor](https://web.archive.org/web/20200928084631/http://planout-editor.herokuapp.com/). For an in-depth look at how we use PlanOut at Facebook, see our paper, [Designing and Deploying Online Field Experiments](https://web.archive.org/web/20200928084631/http://arxiv.org/pdf/1409.3174v1.pdf).

In addition to the Python reference implementation written by Facebook, there are multiple third party ports of PlanOut.

Production-ready ports of PlanOut are available at:

*   [JavaScript](https://github.com/HubSpot/PlanOut.js): complete port of the PlanOut reference implementation to JavaScript. Includes native APIs for ES5 and ES6, as wll as React integration.
    
*   [Java](https://github.com/Glassdoor/planout4j): full-featured implementation of PlanOut by Glassdoor, including experiment lifecycle management and code review.
    
*   [PHP](https://github.com/vimeo/ABLincoln): Vimeo’s implementation of PlanOut. Includes native API with PSR logging.
    

Under development:

*   [Go](https://github.com/URXtech/planout-golang): implementation of PlanOut interpreter for golang.
    
*   [Lua](https://github.com/Fanatics/planout.lua): a complete port of the PlanOut API and language interpreter.
    
*   [Ruby](https://github.com/facebook/planout/tree/master/alpha/ruby): basic native API implementation of PlanOut for Ruby
    

If you are publishing research using PlanOut, please consider referencing our work,

    @inproceedings{bakshy2014www,
    	Author = {Bakshy, E. and Eckles, D. and Bernstein, M. S.},
    	Booktitle = {Proceedings of the 23rd ACM conference on the World Wide Web},
    	Organization = {ACM},
    	Title = {Designing and Deploying Online Field Experiments},
    	Year = {2014}
    }
    

© Copyright 2017, Facebook Inc.
