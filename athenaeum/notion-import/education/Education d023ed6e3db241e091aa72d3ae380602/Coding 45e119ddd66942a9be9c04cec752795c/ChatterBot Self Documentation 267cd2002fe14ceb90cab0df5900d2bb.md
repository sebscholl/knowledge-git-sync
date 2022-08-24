# ChatterBot Self Documentation

Last Edited: December 19, 2019 11:43 PM

Problem: Scoping knowledge graph to individual chatbots that are queryable by name

Created new python class called SingletonBot

SingletonBot has a name, pk, and many to many relationship with both conversations and ID's :

>>> from chatterbot.ext.django_chatterbot.models import SingletonBot

>>> b = SingletonBot()

>>> b

<SingletonBot: >

>>> b.name = "Steve"

>>> b

<SingletonBot: Steve>

>>> b.save()

>>> b

<SingletonBot: Steve>

>>> b.id

1

>>> b.statements

<django.db.models.fields.related_descriptors.create_forward_many_to_many_manager.<locals>.ManyRelatedManager object at 0x109700470>

>>> b.conversations

<django.db.models.fields.related_descriptors.create_forward_many_to_many_manager.<locals>.ManyRelatedManager object at 0x1097608d0>

>>> b.conversations.all()

<QuerySet []>

Updates:

- created AbstractBaseBot Class that can be persisted.
- Creating new trainer to store bot ID along with Statements and responses