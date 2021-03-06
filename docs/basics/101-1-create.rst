.. _createDS:

Starting from scratch: Creating a dataset
-----------------------------------------

We are about to start the eductional course ``DataLad-101``.
In order to follow along and organize course content, let us create
a directory on our computer to collate the materials, assignments, and
notes in.

Since this is ``DataLad-101``, lets do it as a :term:`Datalad dataset`.
You might associate the term "dataset" with a large spreadsheet containing
variables and data.
But for DataLad, as we learned in the first lecture, a dataset is the core data type.

As noted in :ref:`philo`, a dataset is a collection of *files*
in folders, and a file is the smallest unit any dataset can contain.
While it at its core this a very simple concept, datasets come with many
useful features.
Because experiencing is more insightful than just reading, we will explore the
concepts of DataLad datasets together by creating one.

Find a nice place on your computers file system to put a dataset for ``DataLad-101``,
and create a fresh, empty dataset with the ``datalad create`` command.
In a bit of time, you will thank yourself for adding a description about the *location*
of your dataset with the *optional* ``--description`` flag. (At the moment,
we will not dive into the details of where that description ends up or
becomes useful in the future, but in more advanced parts of the book
we will see how this gets handy.)
Note the command structure of ``datalad create`` (optional bits are enclosed in ``[ ]``):

``datalad create [--description "..."] [-c <config options>] PATH``


.. runrecord:: _examples/DL-101_1
   :language: console
   :workdir: dl-101

   $ datalad create --description "course on DataLad-101 on my private Laptop" -c text2git DataLad-101

This will create a dataset called ``DataLad-101`` in the directory you are currently
in. For now, disregard ``-c text2git``. It applies a configuration template, but there
will be other parts of this book to explain this in detail.

Once created, a DataLad dataset looks like any other directory on your filesystem.
Currently, it seems empty.

.. runrecord:: _examples/DL-101_2
   :language: console
   :workdir: dl-101

   $ cd DataLad-101
   $ ls    # ls does not show any output, because the dataset is empty.

However, all files and directories you store within the DataLad dataset
can be tracked (should you want them to be tracked).
*Tracking* in this context means that edits done to a file are automatically
associated with information about the change, the author of the edit,
and the time of this change. This is already informative on its own,
but what is especially helpful is that previous states of files or directories
can be restored. Remember the last time you accidentally deleted content
in a file, but only realized *after* you saved it? With DataLad, no
mistakes are forever. We will see many examples of this later in the book,
and such information is stored in what we will refer
to as the history of a dataset.

This history is almost as small as it can be at the current state, but let's take
a look at it. For looking at the history, the code examples will use ``git log``,
a built-in git command [#f1]_.

.. runrecord:: _examples/DL-101-3
   :language: console
   :workdir: dl-101/DataLad-101
   :emphasize-lines: 3-4, 6, 9-10, 12

   $ git log

We can see two :term:`commit`\s in the history of the repository.
Each of them is identified by a unique 40 character sequence, called a
:term:`checksum`.
Highlighted in this output is information about the author and about
the time, as well as a :term:`commit message` that summarizes the
performed action concisely. In this case, both commit messages were written by
DataLad itself. The most recent change is on the top. The first commit
written to the history therefore states that a new dataset was created,
and the second commit to the history is related to ``-c text2git`` which
uses a configuration template to instruct DataLad to store textfiles
in Git (but more on this later).
Even though these commits were produced by DataLad,
in most other cases, you will have to create the commit and
an informative commit message yourself.

As already noted, any files you ``save`` in this dataset, and all modifications
to these files that you ``save``, are tracked in this history.
Importantly, this file tracking works
regardless of the size of the files - a DataLad dataset could be
your private music or movie collection with single files being many GB in size.
This is one aspect that distinguishes DataLad from many other
version control tools, among them Git.
Large content is tracked in an *annex* that is automatically
created and handled by DataLad. Whether text files or larger files change,
all of these changes can be written to your DataLad datasets history.


.. gitusernote::

   ``datalad create`` uses ``git init`` and ``git-annex init``. Therefore,
   the DataLad dataset is a Git repository.
   Large file content in the
   dataset in the annex is tracked with Git-annex. An ``ls -a``
   reveals that Git is secretly working in the background:

   .. runrecord:: _examples/DL-101-10
      :language: console
      :workdir: dl-101/DataLad-101
      :emphasize-lines: 4-6

      $ ls -a # show also hidden files

   **For non-Git-Users: these hidden** *dot-directories* **are doing their magic in the**
   **background. Please do not temper with them, and, importantly,** *do not delete them.*

Congratulations, you just created your first DataLad dataset!
Let us now put some content inside.



.. todo::

   At some point, dive into how the description of a dataset is used for git-annex and becomes
   handy once git-annex talks to the user, and how it is in git-annex info but nowhere else (?)


.. rubric:: Footnotes

.. [#f1] A nice and easy tool we can recommend as an alternative to ``git log`` is :term:`tig`.
         Once installed, exchange any git log command you see here with the single word ``tig``.
