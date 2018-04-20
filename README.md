# TutorialStack - (c) Andre Lohmann (and others) 2018

## Maintainer Contact
 * Andre Lohmann
   <lohmann.andre (at) gmail (dot) com>

## Content
This repo offers a vagrant machine to showcase a typical DevOps workflow based on gitlab, jenkins, aws, autoscaling, ...

## Requirements

 *  AWS Account
 *  Admin Credentials

## Quickstart
 *  Copy the vars file ansible/vars.yml.example to ansible/vars.yml and fill in the real credentials.
 *  Start the machine with "vagrant up"
 *  the vagrant ansible deployment will create a Bucket and a DynomoDB Table for the Terraform state

## Afterwork
..
